

# Jetpack--(四) ViewBinding优化封装



## 基类BaseActivity封装

```kotlin
abstract class BaseActivity<T: ViewBinding>: AppCompatActivity(){

    lateinit var binding: T

    override fun onCreate(savedInstanceState: Bundle?, persistentState: PersistableBundle?) {
        super.onCreate(savedInstanceState, persistentState)
        binding = getViewBinding()
        setContentView(binding.root)
        initWidgets()
        initData()
    }

    open fun initWidgets(){}

    open fun initData(){}

    abstract fun getViewBinding(): T
}
```

然后在子类中实现

```kotlin
class MainActivity : BaseActivity<ActivityMainBinding>() {
    
    override fun getViewBinding(): ActivityMainBinding = ActivityMainBinding.inflate(layoutInflater)
    
    override fun initWidgets() {
        super.initWidgets()
        binding.textView.apply {
        }
    }

    override fun initData() {
        super.initData()
    }
}
```



## BaseFragment实现

```kotlin
abstract class BaseFragment<T: ViewBinding>: Fragment() {
    lateinit var binding: T

    abstract fun getViewBinding(): T

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        binding = getViewBinding()
        initWidgets()
        initData()
        return binding.root
    }

    /**
     * 初始化View
     */
    open fun initWidgets(){}

    /**
     * 初始化数据
     */
    open fun initData(){}
}
```

用法和BaseActivity一样