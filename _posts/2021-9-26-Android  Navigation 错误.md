---
layout: post

title: Android Navigation错误

categories: Android

description: 

keywords: Android,Navigation

topmost: false





---



## 开发环境:

```shell
Android Studio: 2020.3.1 Patch 1
gradle: 7.0.1
navigation 版本: 2.3.5
```



eg1: 错误详情

```sh
API 'BaseVariant.getApplicationIdTextResource' is obsolete and has been replaced with 'VariantProperties.applicationId'.
It will be removed in version 7.0 of the Android Gradle plugin.

e: /Users/XXX/workspace/Android/demo/NavigationKotlin/app/build/generated/source/navigation-args/debug/com/txh/samples/apps/navigation/LoginFragmentDirections.kt: (12, 16): Class 'ActionLoginFragmentToHomeFragment' is not abstract and does not implement abstract member public abstract val actionId: Int defined in androidx.navigation.NavDirections
```

解决办法： 修改所有配置`navigation`的版本为`2.4.0-alpha08` 或以上，应该是navigation和gradle版本匹配的原因