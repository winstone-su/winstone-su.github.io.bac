---
layout: post
title: Android Studio 和Lombok插件不兼容问题
categories: Android Studio

description: 

keywords: lombok

topmost: false

---



最近安装了高版本的 AS，然后在`Plugins`里已经搜索不到`lombok`这个插件了

在[https://plugins.jetbrains.com/plugin/6317-lombok/versions](https://plugins.jetbrains.com/plugin/6317-lombok/versions)下载离线的安装包

然后报错

```sh
Plugin 'Lombok' (version '0.34.1-2019.1') is not compatible with the current version of the IDE, because it requires build 191.* or older but the current build is AI-211.7628.21
```

解决办法：

 将下载的插件解压，然后拷贝里面的jar包到Android Studio的安装目录 `D:\Program Files\Android\Android Studio\plugins`下面，重启AS即可