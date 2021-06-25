---
layout: post

title: Starting SwiftUI -- 创建表单

categories: SwiftUI

description: 

keywords: Swift,SwiftUI,iOS

topmost: false



---



创建表单

默认文本视图包装在`Form`里面，就可以创建基本表单。

```swift
var body: some View {
    Form {
        Text("Hello SwiftUI 1")
      	Text("Hello SwiftUI 2")
    }
}
```



```sh
tips: 表单最多添加10行，超过10行是不允许的，这是SwiftUI的限制
```



如果表单包含11行及以上内容，需要将内容包裹在`Group`中：

```swift
Form{
            Group{
                Text("Hello SwiftUI 1")
                Text("Hello SwiftUI 2")
                Text("Hello SwiftUI 3")
                Text("Hello SwiftUI 1")
                Text("Hello SwiftUI 2")
                Text("Hello SwiftUI 3")
                Text("Hello SwiftUI 1")
                Text("Hello SwiftUI 2")
                Text("Hello SwiftUI 3")
                Text("Hello SwiftUI 1")
            }
            
            Group{
                Text("Hello SwiftUI 4")
                Text("Hello SwiftUI 5")
                Text("Hello SwiftUI 6")
            }
        }
```

`Group`实际上不会改变用户界面的外观，它们只是让我们绕过SwiftUI在父视图中只包含10个子视图的限制

如果希望拆分表单成块，应该用`Section`视图

```swift
Form{
                Section{
                    Text("Hello SwiftUI 1")
                    Text("Hello SwiftUI 2")
                    Text("Hello SwiftUI 3")
                }
                Section{
                    Text("Hello SwiftUI 4")
                    Text("Hello SwiftUI 5")
                    Text("Hello SwiftUI 6")
                }
 }
```

![img]({{site.url }}/assets/images/202103/0310-01.png)

