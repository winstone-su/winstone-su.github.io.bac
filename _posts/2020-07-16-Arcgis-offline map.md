---
layout: post
title: Arcgis offline map
categories: Arcgis
description: 
keywords: iOS,Swift,Arcgis
topmost: false
---

加载离线地图:

```Swift
private let mobileMapPackage = AGSMobileMapPackage(name: "offline-maps-package")
    
    private func setupMap() {
        mobileMapPackage.load { [weak self](error) in
            guard let self = self else {return}
            if let error = error {
                print("Error loading the mobile map package: \(error.localizedDescription)")
                return
            }else if let map = self.mobileMapPackage.maps.first{
                self.mapView.map = map
            }
        }
    }
```



