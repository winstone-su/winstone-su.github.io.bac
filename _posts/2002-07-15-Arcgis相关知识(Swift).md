---
layout: post

title: Arcgis相关知识

categories: Arcgis

description:  Arcgis Sample Swift

keywords: iOS,Arcgis

topmost: false
---



​	AGS相关知识:

 * 添加一个 `GraphicsOverlay`

    * 点

      ```swift
      let graphicsOverlay = AGSGraphicsOverlay()
              mapView.graphicsOverlays.add(graphicsOverlay)
              
              let ref:AGSSpatialReference = .wgs84()
              
              let pointGraphic: AGSGraphic = {
                  //Create a point geometry
                  let point = AGSPoint(x: 111.677914, y: 40.838096, spatialReference: ref)
                  //Create point symbol with outline 
                	// style: 中心点的样式
                  let symbol = AGSSimpleMarkerSymbol(style: .diamond, color: .orange, size: 10.0)
                  //设置边线的样式
                  symbol.outline = AGSSimpleLineSymbol(style: .solid, color: .blue, width: 2.0)
                //let textSymbol = AGSTextSymbol(text: "This is textSymbol", color: .red, size: 10.0, horizontalAlignment: .left, verticalAlignment: .middle)
                  
                  //Create point graphic with geometry & symbol
                  return AGSGraphic(geometry: point, symbol: symbol, attributes: nil)
              }()
              
              graphicsOverlay.graphics.add(pointGraphic)
      ```

      

      * 线

        ```swift
        let lineGraphic:AGSGraphic = {
                   let polyline = AGSPolyline(
                        points:[
                            AGSPoint(x: 111.681234, y: 40.839142, spatialReference: ref),
                            AGSPoint(x: 111.691345, y: 40.847132, spatialReference:ref)
                        ]
                    )
                    
                    let polylineSymbol = AGSSimpleLineSymbol(style:.solid, color: .orange, width: 4.0)
                    
                    return AGSGraphic(geometry: polyline, symbol: polylineSymbol, attributes: nil)
                }()
                
                graphicsOverlay.graphics.add(lineGraphic)
        ```

        

      * 面

        ```swift
        let polygonGraphic: AGSGraphic = {
                    let polygon = AGSPolygon(points: [
                        AGSPoint(x: 111.683211, y: 40.839132, spatialReference: ref),
                        AGSPoint(x: 111.703211, y: 40.840142, spatialReference: ref),
                        AGSPoint(x: 111.710211, y: 40.831023, spatialReference: ref)
                    ])
                    
                    let polygonSymbol = AGSSimpleFillSymbol(style: .solid, color: .red,
                                                            outline: AGSSimpleLineSymbol(
                                                                style: .solid, color: .blue, width: 3.0
                        )
                    )
                    
                    return AGSGraphic(geometry: polygon, symbol: polygonSymbol, attributes: nil)
                }()
                
                graphicsOverlay.graphics.add(polygonGraphic)
        ```

