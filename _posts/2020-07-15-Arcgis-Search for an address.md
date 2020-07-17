---
layout: post

title: Arcgis-Search for an address

categories: Arcgis,ios

description: Arcgis Sample Swift

keywords: iOS,Arcgis,Swift

topmost: false
---

Link: https://developers.arcgis.com/labs/ios/search-for-an-address/

```Swift
let geocoder:AGSLocatorTask = AGSLocatorTask(url: URL(string: "https://geocode.arcgis.com/arcgis/rest/services/World/GeocodeServer")!)
```

```Swift
func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        guard let searchText = searchBar.text, !searchText.isEmpty else {
            print("Nothing to search")
            return
        }
        
        geocoder.geocode(withSearchText: searchText) { (results, error) in
            guard error == nil else{
                print("Error Geocoding `\(searchText)`: \(error!.localizedDescription)")
                return
            }
            
            guard let  firstResult = results?.first, let extent = firstResult.extent else{
                let alert = UIAlertController(title: "Nothing Found", message: "No results  found for \(searchText)", preferredStyle: .alert)
                alert.addAction(UIAlertAction(title: "OK", style: .default, handler: { (_) in
                    alert.dismiss(animated: true, completion: nil)
                }))
                self.present(alert, animated: true, completion: nil)
                return
            }
            //将获取到的geometry加载到地图上
            let point:AGSPoint = firstResult.displayLocation!
            let simpleMarkSymbol = AGSSimpleMarkerSymbol(style: .circle, color: .red, size: 10)
            
            let resultGraphics = AGSGraphic(geometry: point, symbol:simpleMarkSymbol , attributes: nil)
            self.mGraphicsOverlay.graphics.add(resultGraphics)
            
            
            self.mapView.setViewpointGeometry(extent, completion: nil)
        }
    }
```

