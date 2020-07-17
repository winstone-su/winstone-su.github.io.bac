---
layout: post
title: Arcgis-Find Places
categories: Arcgis
description: 
keywords: iOS,Swift,Arcgis
topmost: false
---



```swift
//
//  ViewController.swift
//  ArcgissSampleFive
//
//  Created by geowin on 2020/7/15.
//  Copyright © 2020 geowin. All rights reserved.
//

import UIKit
import ArcGIS

class ViewController: UIViewController ,UIPickerViewDataSource,UIPickerViewDelegate{

    func numberOfComponents(in pickerView: UIPickerView) -> Int {
        1
    }
    
    func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {
        Category.all.count
    }
    
    func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {
        Category.all[row].title
    }
    
    func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
        findPlaces(forCategory: Category.all[row])
    }
    
    
    @IBOutlet weak var mapView: AGSMapView!
    
    @IBOutlet weak var categoryPicker: UIPickerView!
    
    private let placesOverlay = AGSGraphicsOverlay()
    private let locatorTask = AGSLocatorTask(url: .locator)
    private var currentSearch: AGSCancelable?
    private var isNavigatingObservation: NSKeyValueObservation?
    private var visibleAreaObservation: NSKeyValueObservation?
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        initialMap()
        /// Add Observe
        observeChangesInMapViewIsNavigating()
        observeChangesInMapViewVisibleArea()
    }
    
    private func observeChangesInMapViewIsNavigating() {
        // The map view `.isNavigating` property determines if the map view's visible area has changed.
        isNavigatingObservation = mapView.observe(\.isNavigating) { [weak self] (mapView, _) in
            // Find places for a selected category when the map view stops navigating.
            guard !mapView.isNavigating else { return }
            // Update results if the map view extent has moved.
            self?.findPlacesForCategoryPickerSelection()
        }
    }
    
    private func observeChangesInMapViewVisibleArea() {
        // Use the map view `.visibleArea` property to observe when the view sets its visible area for the first time.
        visibleAreaObservation = mapView.observe(\.visibleArea) { [weak self] (mapView, _) in
            guard let self = self else { return }
            // When the visible area is set for the first time, kick off the first find places query.
            self.findPlacesForCategoryPickerSelection()
            // Nullify (thus invalidating) the visible area observation because the first find places query is performed.
            self.visibleAreaObservation = nil
        }
    }
    
    // MARK:- 初始化地图
    func initialMap(){
//        let tiledLayer = `AGSArcGISTiledLayer`(url: URL(string: "http://map.geoq.cn/ArcGIS/rest/services/ChinaOnlineCommunity/MapServer")!)
//
//        let map = AGSMap(basemap: AGSBasemap(baseLayer: tiledLayer))
//        let location = CLLocationCoordinate2D(latitude: 40.838096, longitude: 111.677914)
//        let center = AGSPoint(clLocationCoordinate2D: location)
//        map.initialViewpoint = AGSViewpoint(center: center, scale: 20000)
//        mapView.map = map
        
        mapView.map = AGSMap(basemapType: .navigationVector, latitude: 34.09042, longitude: -118.71511, levelOfDetail: 10)
        
        mapView.graphicsOverlays.add(placesOverlay)
        
        mapView.touchDelegate = self
        
    }
    
    func addPlacesGraphics(_ results: [AGSGeocodeResult],for category: Category){
        // Build place marker symbol.
        let symbol: AGSSimpleMarkerSymbol = {
            let placeSymbol = AGSSimpleMarkerSymbol(style: .circle, color: category.color, size: 10.0)
            placeSymbol.outline = AGSSimpleLineSymbol(style: .solid, color: .white, width: 2)
            return placeSymbol
        }()
        // Represent each place as a dot on the map.
        // Each graphic symbol gets the place attributes and later shows them when the user taps the graphic.
        let places = results.map { (result) in
            AGSGraphic(geometry: result.displayLocation, symbol: symbol, attributes: result.attributes)
        }
        
        placesOverlay.graphics.addObjects(from: places)
    }
    
    
    func clearPlacesGraphics(){
        placesOverlay.graphics.removeAllObjects()
    }
    
    func showCallout(for graphic: AGSGraphic){
        mapView.callout.title = graphic.attributes[String.placeName] as? String ?? "Unknown"
        mapView.callout.detail = graphic.attributes[String.placeAddress] as? String ?? "no address provided"
        mapView.callout.show(for: graphic, tapLocation: graphic.geometry as? AGSPoint, animated: true)
    }
    
    func hideCallout(){
        if mapView != nil {
            mapView.callout.dismiss()
        }
    }
    
    func findPlaces(forCategory category: Category){
        guard let visibleArea = mapView.visibleArea else {return}
        
        hideCallout()
        clearPlacesGraphics()
        
        currentSearch?.cancel()
        
        let paramters: AGSGeocodeParameters = {
            let geocodeParameters = AGSGeocodeParameters()
            geocodeParameters.maxResults = 25
            geocodeParameters.resultAttributeNames.append(contentsOf: [. placeAddress,.placeName])
            geocodeParameters.preferredSearchLocation = visibleArea.extent.center
            geocodeParameters.categories = [category.title]
            return geocodeParameters
        }()
        
        
        currentSearch = locatorTask.geocode(withSearchText: "", parameters: paramters, completion: {
            [weak self] (result, error) in
            guard let self = self else {return}
            guard error == nil else{
                print("Geocode error: ",error!.localizedDescription)
                return
            }
            
            guard let result = result,result.count > 0 else{
                print("No places found for category ",category.title)
                return
            }
            
            self.addPlacesGraphics(result, for: category)
        })
    }
    
    private func findPlacesForCategoryPickerSelection(){
        DispatchQueue.main.async {  [weak self] in
            guard let self = self else {return}
            let categoryIndex = self.categoryPicker.selectedRow(inComponent: 0)
            guard categoryIndex < Category.all.count else {return}
            let category = Category.all[categoryIndex]
            self.findPlaces(forCategory: category)
        }
    }
}

extension ViewController: AGSGeoViewTouchDelegate{
    
    func geoView(_ geoView: AGSGeoView, didTapAtScreenPoint screenPoint: CGPoint, mapPoint: AGSPoint) {
        hideCallout()
        
        mapView.identify(placesOverlay, screenPoint: screenPoint, tolerance: 10, returnPopupsOnly: false, maximumResults: 1) { [weak self](result) in
            guard let self = self else { return }
            if let error = result.error{
                print(error)
                return
            }
            else if let graphic = result.graphics.first{
                self.showCallout(for: graphic)
            }
        }
    }
}

```

