



# Kotlin基础 - infix关键字

 `infix`关键字适用于有单个参数的扩展和类函数，可以让你以更简洁的语法调用函数，如果一个函数定义使用了infix关键字，那么调用它时，接受者和函数之间的点操作以及参数的一对括号都可以不要。

参考

```kotlin
public infix fun <A, B> A.to(that: B): Pair<A, B> = Pair(this, that)
//使用 
mapOf("Lee" to "23")
```

自定义一个infix函数

```kotlin
infix fun String?.printWithDefault(default: String) {
    println(this ?: default)
}
//使用以下两种方法都可以
fun main() {
    "hfer".printWithDefault("hello")
    "we" printWithDefault "me"
}
```

