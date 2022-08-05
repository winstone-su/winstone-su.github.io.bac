---
layout: post

title: Jetpack -- (三)LiveData

categories: Kotlin

description: 

keywords: Kotlin,Android,Jetpack

topmost: false



---

# Jetpack --(三)LiveData



### 简单使用

场景： 定时修改 textView的值

```kotlin
class TextViewModel: ViewModel() {
    private val _currentSecond = MutableLiveData<Int>()

    val currentSecond: MutableLiveData<Int>
        get() = _currentSecond

    init {
        _currentSecond.value = 0
    }

    fun addSecond(){
        _currentSecond.postValue(_currentSecond.value?.plus(1))
    }
}
```



```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    private lateinit var viewModel: TextViewModel
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)

        viewModel = ViewModelProvider(this)[TextViewModel::class.java]
        binding.textView.text = viewModel.currentSecond.value.toString()
        //添加观察
        viewModel.currentSecond.observe(this){
            binding.textView.text = viewModel.currentSecond.value.toString()
        }
        startTimer()
    }

    private fun startTimer(){
        Timer().schedule(object: TimerTask() {
            override fun run() {
                viewModel.addSecond()
            }
        },1000L,1000L)
    }
}
```

修改livedata的值，需要注意

* postValue 非UI线程
* setValue  UI线程

```java
 protected void postValue(T value) {
        boolean postTask;
        synchronized (mDataLock) {
            postTask = mPendingData == NOT_SET;
            mPendingData = value;
        }
        if (!postTask) {
            return;
        }
        ArchTaskExecutor.getInstance().postToMainThread(mPostValueRunnable);
    }
```

可以看到，其实postValue 最后还是回到主线程

### ViewModel + LiveData实现Fragment间通信

使用场景： 构建两个Fragment，里面都只包含一个SeekBar，拖动seekbar，另一个fragmetn的seekbar也随之拖动

```kotlin
class MyViewModel: ViewModel() {

    private val _progress = MutableLiveData<Int>()

    val progress: MutableLiveData<Int>
        get() = _progress

    init {
        _progress.value = 0
    }
}
```

Fragment

```kotlin
class FirstFragment : Fragment() {

    private var _binding: FragmentFirstBinding? = null

    private val binding get() = _binding!!

    private val myViewModel: MyViewModel by activityViewModels()
    
    override fun onCreateView(
        inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View? {
        // Inflate the layout for this fragment
        _binding = FragmentFirstBinding.inflate(inflater,container,false)

        //TODO : 注意这里的owner
        myViewModel.progress.observe(viewLifecycleOwner){
            binding.seekBar.progress  = it
        }

        Log.e("TAG", "onCreateView: $myViewModel" )

        binding.seekBar.apply {
            setOnSeekBarChangeListener(object : SeekBar.OnSeekBarChangeListener{
                override fun onProgressChanged(p0: SeekBar?, p1: Int, p2: Boolean) {
                    myViewModel.progress.value = p1
                }

                override fun onStartTrackingTouch(p0: SeekBar?) {

                }

                override fun onStopTrackingTouch(p0: SeekBar?) {

                }
            })

        }
        return binding.root
    }

    override fun onDestroyView() {
        super.onDestroyView()
        _binding = null
    }

}
```

