



# Kotlin: Retrifit解析数据包含enum类型



**在项目中经常会遇到服务端返回的字段是 int类型，用来区分不同的状态，但是前端如果直接写 if( xx == 1) else if( xx == 2 )这样的判断，代码格式不美观，而且也容易出错,因此可以在定义数据结构的时候可以增加enum类型来判断 状态**

Json数据

```json
{
    "id":100101,
    "status":1,
    "url":"http://www.baidu.com"
}
```

数据结构：

```kotlin

data class TaskResponse(
    val id: Int,
    val url: String,
    var photoStatus: PhotoStatus
)

enum class PhotoStatus(val key: Int,val valueText: String) {
    @SerializedName("0") //注意这里的序列化必须添加
    UN_PHOTOGRAPHED(0,"未拍照"),
    @SerializedName("1")
    PHOTOGRAPHED(1,"已拍照")
}
```

注意：**枚举类`PhotoStatus`中属性 需要加上 @SerializedName()的注解，不然会出现 `status = null`的情况**

而且在处理 `status`字段的时候，可以利用 `when`表达式来处理，更加方便

```kotlin
when(photoStatus) {
            PhotoStatus.UN_PHOTOGRAPHED -> {} //photoStatus.valueText: String
            PhotoStatus.PHOTOGRAPHED ->  {}  //photoStatus.key: Int
}
```

