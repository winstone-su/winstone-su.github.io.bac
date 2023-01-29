

# Android Studio 导入项目错误 has been compiled by a more recent version of the Java Runtime



错误日志：

```kotlin
has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0
```

原因：`JDK版本不对`,对照关系如下

```shell
50	-->	JDK1.6
51	-->	JDK1.7
52	-->	JDK1.8
53	-->	JDK  9
54	-->	JDK 10
55	-->	JDK 11
56	-->	JDK 12
57	-->	JDK 13
58	-->	JDK 14
59	-->	JDK 15

```

