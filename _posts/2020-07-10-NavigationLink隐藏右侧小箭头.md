---

layout: post

title:  NavigationLink隐藏右侧小箭头

categories: Swift

description: 

keywords: Swift,NaavigationLink

topmost: false

---

​	在使用	NavigationLink的时候发现，默认右侧会带上一个小箭头

![landmarks]({{ site.url }}/assets/images/landmarks.png)

解决办法:

```swift
        NavigationView {
            List(landmarkData) { landmark in
                ZStack{
                    LandmarkRow(landmark: landmark)
                    NavigationLink(destination: LandmarkDetail(landmark: landmark)) {
                        EmptyView()
                    }
                }
            }
            .navigationBarTitle(Text("Landmarks"))
        }
```

