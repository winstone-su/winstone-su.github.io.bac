---
layout: post

title: Starting SwiftUI -- NavigationBar

categories: SwiftUI

description: 

keywords: Swift,SwiftUI,iOS

topmost: false




---



默认情况下，iOS允许我们在屏幕上的任何地方放置内容，包括在系统时钟和主指示器下。这看起来不太好，这就是为什么默认情况下，SwiftUI会确保组件放置在系统UI或设备圆角无法覆盖的区域中，这一区域称为安全区域。

在iPhone 11上，安全区域的范围从略低于刘海到略高于主指示器（底部白条）。您可以在这样的用户界面中看到它的运行：

```swift
struct ContentView: View {
    var body: some View {
        Form{
            Section{
                Text("Hello Swift")
            }
        }
    }
}
```

表单是可以上下滚动的，向上滑动的时候，状态栏可能会覆盖表单，影响阅读。

常见的解决办法是，在顶部增加一个导航栏`NavagationView`。导航栏有标题和按钮，在SwiftUI中，它们还让我们能够在用户执行操作时显示新视图。

```swift
struct ContentView: View {
    var body: some View {
        NavigationView{
            Form{
                Section{
                    Text("Hello SwiftUI 1")
                    Text("Hello SwiftUI 2")
                    Text("Hello SwiftUI 3")
                }
            }
        }
    }
}
```

我们尝试添加一个修饰符来添加导航栏标题:

```swift
NavigationView{
            Form{
                Section{
                    Text("Hello SwiftUI 1")
                    Text("Hello SwiftUI 2")
                    Text("Hello SwiftUI 3")
                }
            }
            .navigationTitle("SwiftUI")
        }
```

也可以在右侧的视图检查器中操作：

将光标放在`Form`表单处，在视图检查器中的 `Add Modifier`中搜索`Navagation Title` 输入`SwiftUI`

![img]({{site.url }}/assets/images/202103/0310-02.png)

当我们将`.navigationBarTitle()`修饰符附加到表单时，Swift实际上会创建一个新表单，该表单具有导航栏标题和您提供的所有现有内容。

将标题添加到导航栏时，您会注意到该标题使用了大字体。您可以使用稍微不同的`navigationBarTitle（）`调用获得一个小字体：

```swift
.navigationBarTitle("SwiftUI",displayMode: .inline)
```

或者:

```swift
.navigationTitle("SwiftUI")
.navigationBarTitleDisplayMode(.inline)
```

