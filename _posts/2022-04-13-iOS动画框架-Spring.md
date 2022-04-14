---
layout: post

title: iOS动画框架-Spring

categories: iOS,Swift

description: 

keywords: iOS,Swift,Animation

topmost: false




---

### 框架地址

```xml
https://github.com/MengTo/Spring
```

### 安装方法

* Cocoapods: (推荐)

  ```xml
  use_frameworks!
  pod 'Spring', :git => 'https://github.com/MengTo/Spring.git'
  ```

* 手动安装：

  将`Spring` 文件夹拖进Xcode工程,确保勾选了(`Copy Item if nedd ` 和 `Create groups`)

### 使用方法

* 代码：

  ```swift
  springView.animation = "shake"
  springView.animate()
  ```

* Storyboard

  选择`View` 的类型

  <img src="https://gitee.com/sliverfoxwb/image/raw/master/img/Screen Shot 2022-04-13 at 17.46.11.png" alt="class" style="zoom:67%;" />

  可以在`Attribute Inspector`中设置属性

  <img src="https://gitee.com/sliverfoxwb/image/raw/master/img/Screen Shot 2022-04-14 at 09.55.52.png" alt="Attribute Inspector" style="zoom:67%;" />

  

  

  