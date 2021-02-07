---
layout: post
title: Arcgis for Android 100.10.0(一)：开发环境配置
categories: ArcgisForAndroid
description: Arcgis,Android
keywords: Android,Arcgis
topmost: false

---

### (一)  在`Project`的`build.gradle`文件中中进行配置:

```java
allprojects {
    repositories {
        google()
        jcenter()

        // Add the following ArcGIS repository
        maven {
            url 'https://esri.bintray.com/arcgis'
        }
    }
}
```



### (二) 在`Module`的`build.gradle`中添加依赖:

```java
// Add ArcGIS Runtime SDK for Android dependency
implementation 'com.esri.arcgisruntime:arcgis-android:100.10.0'
```

### (三) 在`Module`的`builde.gradle`的`android`中添加配置:

```java
android {
    compileSdkVersion 30
    buildToolsVersion "30.0.2"

     //Add Arcgis compile sdk
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
 }
```

### (四) 在`AndroidManifest.xm`l中添加:

```xml
<uses-permission android:name="android.permission.INTERNET" />
    <uses-feature
        android:glEsVersion="0x00020000"
        android:required="true" />
```

