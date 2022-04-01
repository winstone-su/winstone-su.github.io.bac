---
layout: post
title: Arcgis Runtime API for Android 100.13 (一)环境配置
categories: Arcgis for Android

description: 

keywords: Arcgis,Android

topmost: false


---

# 环境配置

1.低版本的Gradle,在  `build.gradle` 的`repositories` 里配置

高版本的Gradle,在`settings.gradle`里的`dependencyResolutionManagement`里配置

```shell
 repositories {
        google()
        mavenCentral()
        maven {
            url 'https://esri.jfrog.io/artifactory/arcgis'
        }
    }
```

2.在`Module`的`build.gradle`里配置

```shell
 implementation 'com.esri.arcgisruntime:arcgis-android:100.13.1'
```

3.在`Module` `build.gradle`里配置Java8

```shell
android {
  ...
  compileOptions {
    sourceCompatibility 1.8
    targetCompatibility 1.8
  }
}
```

4.在`Module` `build.gradle`中添加

```shell
android {
  ...
  packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
	}
}

```



