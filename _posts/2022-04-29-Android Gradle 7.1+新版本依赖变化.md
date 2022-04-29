---
layout: post

title: Android Gradle 7.1+新版本依赖变化

categories: Android

description: 

keywords: Android,Hilt,gradle

topmost: false




---

## 

## Android Gradle 7.1+新版本依赖变化



### 1.功能位置迁移

旧版 `Project build.gradle`的 `buildscript`和 `allprojects`的移动至`setting.gradle`并改名为`pluginManagement`和`dependencyResolutionManagement`

```kotlin
pluginManagement {
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
    }
}
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
    }
}
rootProject.name = "Hilt"
include ':app'
```

***如果修改rootProject.name的内容，会在当前工程下新建该内容的文件夹，把原来的文件夹内容移动到新文件夹中***

### 2. dependencies变化

​	`Project/build.gradle`文件中之前的dependencies文件

```groovy
dependencies {
    classpath "com.android.tools.build:gradle:7.0.3"
    // NOTE: Do not place your application dependencies here; they belong
    // in the individual module build.gradle files
}
```

变为：

```groovy
plugins {
    id 'com.android.application' version '7.1.3' apply false
    id 'com.android.library' version '7.1.3' apply false
    id("org.jetbrains.kotlin.android") version "1.5.30" apply false
}
```

## 引入`Hilt`依赖的变化

在`Module/build.gradle`中：

```groovy
plugins {
    id 'com.android.application'
    id 'kotlin-android'
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}
```

依赖中添加:

```groovy
dependencies {
    implementation 'androidx.appcompat:appcompat:1.4.1'
		...
		//Hilt支持
    implementation "com.google.dagger:hilt-android:2.28-alpha"
    kapt "com.google.dagger:hilt-android-compiler:2.28-alpha"

}
```



**最重要的一步**

在`setting.gradle`中添加`resolutionStrategy`

```groovy
pluginManagement {
    resolutionStrategy{
        eachPlugin {
            if( requested.id.id == 'dagger.hilt.android.plugin') {
                useModule("com.google.dagger:hilt-android-gradle-plugin:2.28-alpha")
            }
        }
    }
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
    }
}
```


Done!