---
layout: post

title: Starting SwiftUI -- Modifying Program State

categories: SwiftUI

description: 

keywords: Swift,SwiftUI,iOS

topmost: false

---

在SwiftUI开发人员中有一种说法是，我们的“视图是他们状态的函数(views are a function of their state)”，但这虽然只是少数几句话，但一开始对您来说可能毫无意义。

如果您正在玩格斗游戏，那么您可能会丧生，夺取一些积分，收集一些财宝，甚至可能会捡起一些强大的武器。在编程中，我们称这些为*状态*-描述游戏当前*状态*的有效设置集合。

当您退出游戏时，该状态将被保存，并且当您稍后返回游戏时，您可以重新加载游戏以回到原来的状态。但是，*在*您玩游戏时，这全都叫做*state*：所有整数，字符串，布尔值等等，都存储在RAM中以描述您现在正在做什么。

当我们说SwiftUI的视图是其状态的函数时，我们的意思是用户界面的外观（人们可以看到的东西以及可以与之交互的东西）由程序的状态决定。例如，他们只有在文本字段中输入自己的姓名后才能点击“继续”。

这本身听起来似乎很明显，但这实际上与之前使用的替代方案有很大不同：您的用户界面由一系列事件决定。因此，用户现在看到的是因为他们已经使用您的应用程序已有一段时间，利用了各种功能，可能已经登录或刷新了数据，等等。

“事件顺序”方法意味着很难存储应用程序的状态，因为获取完美状态的唯一方法是回放用户执行的事件的确切顺序。这就是为什么如此多的应用程序甚至根本不尝试保存状态的原因-您的新闻应用程序将不会返回到您正在阅读的上一篇文章，Twitter不会记住您是否正在键入内容。回复某人，Photoshop会忘记您堆积的任何撤消状态。

让我们通过一个按钮将其付诸实践，该按钮可以在SwiftUI中使用标题字符串和一个动作闭合创建，并在按下按钮时运行该闭合：

```swift
struct ContentView: View {
    var tapCount = 0

    var body: some View {
        Button("Tap Count: \(tapCount)") {
            self.tapCount += 1
        }
    }
}
```

该代码看起来足够合理：创建一个显示“点击计数”的按钮，再加上点击该按钮的次数，然后在`tapCount`每次点击该按钮时加1 。

但是，它不会建立。那不是有效的Swift代码。您看到的`ContentView`是一个结构，可以将其创建为常量。如果回想起当您了解结构时，这意味着它是*不可变的*–我们不能随意更改其值。

例如，在创建要更改属性的结构方法时，我们需要添加`mutating`关键字：`mutating func doSomeWork()`。但是，Swift不允许我们对计算的属性进行突变，这意味着我们不能编写`mutating var body: some View`-只是不允许这样做。

似乎我们陷入了僵局：我们希望能够在程序运行时更改值，但是Swift不允许我们这样做，因为我们的视图是结构。

幸运的是，Swift为我们提供了一个特殊的解决方案，称为*属性包装器*：可以在属性之前放置一个特殊的属性，以有效地赋予它们超能力。在存储简单的程序状态（如点击按钮的次数）的情况下，我们可以使用来自SwiftUI的名为的属性包装器`@State`，如下所示

```swift
struct ContentView: View {
    @State var tapCount = 0

    var body: some View {
        Button("Tap Count: \(tapCount)") {
            self.tapCount += 1
        }
    }
}
```

这个很小的变化足以使我们的程序正常工作，因此您现在可以构建它并进行尝试。

`@State`允许我们解决结构的局限性：我们知道由于结构是固定的，我们无法更改其属性，但`@State`允许该值由SwiftUI单独存储在*可以*修改的位置。

是的，感觉有点像作弊，您可能想知道为什么我们不使用类，而是*可以*自由修改它们。但是请相信我，这是值得的：随着您的进步，您将了解到SwiftUI经常破坏并重新创建您的结构，因此将它们保持为较小且简单的结构对于性能至关重要。

**提示：**有几种方法可以在SwiftUI中存储程序状态，您将学习所有这些方法。`@State`专为存储在一个视图中的简单属性而设计。因此，Apple建议我们`private`向这些属性添加访问控制，如下所示：`@State private var tapCount = 0`。

译: [Modifying Program State](https://www.hackingwithswift.com/books/ios-swiftui/modifying-program-state)