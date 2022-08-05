---
layout: post

title: Jetpack -- (二)ViewModel

categories: Kotlin

description: 

keywords: Kotlin,Android,Jetpack

topmost: false


---

# Jetpack --(二) ViewModel

ViewModel的诞生:

* 瞬态数据丢失
* 异步调用的内存泄漏
* 类膨胀提高维护难度和测试难度



添加依赖

```groovy
implementation 'androidx.lifecycle:lifecycle-viewmodel-ktx:2.5.1'
```

* 不要向ViewModel中传入Context，会导致内存泄漏
* 如果要使用Context，请使用AndroidViewModel中的Application

简单应用：

```kotlin
class MyViewModel: ViewModel() {

    var num:Int = 0

}
```

```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    private lateinit var viewModel: MyViewModel
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        viewModel = ViewModelProvider(this)[MyViewModel::class.java]
//        viewModel = ViewModelProvider(this,ViewModelProvider.AndroidViewModelFactory(this.application))[MyViewModel::class.java]

        binding.textView.text = viewModel.num.toString()

        binding.button.setOnClickListener{
            viewModel.num += 1
            binding.textView.text = viewModel.num.toString()
        }
    }
}
```

在Fragment中使用ViewModel

```kotlin
private lateinit var myViewModel: MyViewModel
myViewModel = ViewModelProvider(this)[MyViewModel::class.java]
```



### 在Activity中使用委托

导入依赖:

```groovy
 implementation 'androidx.activity:activity-ktx:1.6.0-alpha05'
```

```kotlin
private  val viewModel: MyViewModel by viewModels()
```

或者直接使用

```kotlin
val viewModel by lazy {
        ViewModelProvider(this)[MyViewModel::class.java]
    }
```

### 在Fragment中使用委托

添加依赖

```
implementation "androidx.fragment:fragment-ktx:1.5.1"
```

使用：

```kotlin
private val myViewModel: MyViewModel by activityViewModels()
```

