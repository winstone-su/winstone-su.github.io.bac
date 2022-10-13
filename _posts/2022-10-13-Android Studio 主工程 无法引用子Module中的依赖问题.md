

# Android Studio 主工程 无法引用子Module中的依赖问题



最近在构建Android项目的时候发现，主工程无法引用子Module中的依赖。

处理方法： 在子`module`的`build.gradle`中对第三方库得依赖方式从`implementation`为`api`

```shell
implementation "com.squareup.retrofit2:retrofit:2.9.0"
//改为
api "com.squareup.retrofit2:retrofit:2.9.0"
```

