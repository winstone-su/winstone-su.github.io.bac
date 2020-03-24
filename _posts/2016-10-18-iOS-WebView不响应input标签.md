---
layout: post
title: "iOS WebView不响应input标签"
date: 2016-10-18 15:59:04 
description: "iOS WebView不响应input标签"
tag: iOS

---

遇到一个超级坑的问题，一个普通的HTML里面有一个上传图片的功能，用了这个标签，点击标签可以弹出选择图片的actionsheet.

![ActionSheet](http://img.blog.csdn.net/20161018160427673 "Photo Library")

但是点了选项只有没有任何反应，还会关闭当前的webview 

在点了标签后，调试会报出以下错误


	Passed in type public.item doesn't conform to either public.content or public.data. If you are exporting a new type, please ensure that it conforms to an appropriate parent type.
	the behavior of the UICollectionViewFlowLayout is not defined because:
	the item width must be less than the width of the UICollectionView minus the section insets left and right values, minus the content insets left and right values.
	The relevant UICollectionViewFlowLayout instance is <_UIAlertControllerCollectionViewFlowLayout: 0x7fd0585c9fb0>, and it is attached to <UICollectionView: 0x7fd058837800; frame = (0 44; 10 0); clipsToBounds = YES; gestureRecognizers = <NSArray: 0x7fd0585cacf0>; animations = { bounds.origin=<CASpringAnimation: 0x7fd05a83daf0>; bounds.size=<CASpringAnimation: 0x7fd05a83e2c0>; position=<CASpringAnimation: 0x7fd05a83e450>; }; layer = <CALayer: 0x7fd0585ca830>; contentOffset: {0, 0}; contentSize: {0, 0}> collection view layout: <_UIAlertControllerCollectionViewFlowLayout: 0x7fd0585c9fb0>.
	Make a symbolic breakpoint at UICollectionViewFlowLayoutBreakForInvalidSizes to catch this in the debugger.


然后各种查看这个错误，发现我的这个webviewController是present进来的，然后把进入方式改成pushviewController就可以了

参考链接: [http://stackoverflow.com/questions/25942676/ios-8-sdk-modal-uiwebview-and-camera-image-picker][jekyll-docs]


[jekyll-docs]: http://stackoverflow.com/questions/25942676/ios-8-sdk-modal-uiwebview-and-camera-image-picker
