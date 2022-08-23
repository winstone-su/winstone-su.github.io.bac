---
layout: post

title: Jetpack -- (一)Lifecycle

categories: Kotlin

description: 

keywords: Kotlin,Android,Jetpack

topmost: false



---

# Jetpack -- (一)Lifecycle



## 使用Lifecycle解耦页面与组件

### 场景： Chronometer统计页面在前台时间

使用Lifecycle之前：

```kotlin
private lateinit var binding: ActivityMainBinding

    private var elapsedTime:Long = 0

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
    }

    override fun onResume() {
        super.onResume()
        binding.chronometer.apply {
            base = SystemClock.elapsedRealtime()
            start()
        }
    }

    override fun onPause() {
        super.onPause()
        binding.chronometer.apply {
            elapsedTime = SystemClock.elapsedRealtime() - base
            stop()
        }
    }
```

使用Lifecycle之后:

```kotlin
class MyChronometer(context: Context, attrs: AttributeSet) : Chronometer(context, attrs),LifecycleEventObserver {
    private var elapsedTime: Long = 0

    private fun startMeter() {
        base = SystemClock.elapsedRealtime() - elapsedTime
        start()
    }

    private fun stopMeter() {
        elapsedTime = SystemClock.elapsedRealtime() - this.base
        stop()
    }

    override fun onStateChanged(source: LifecycleOwner, event: Lifecycle.Event) {
        when (event) {
            Lifecycle.Event.ON_RESUME -> startMeter()
            Lifecycle.Event.ON_PAUSE -> stopMeter()
        }
    }
}
```

同时需要在Activity的`onCreate()`中添加:

```kotlin
 lifecycle.addObserver(binding.chronometer)
```



## 使用LifecycleService解耦Service与组件

添加依赖:

```sh
implementation 'androidx.lifecycle:lifecycle-extensions:2.2.0'
```

Observer

```kotlin
class LocationObserver(serviceContext: Context) : DefaultLifecycleObserver {
    companion object{
        private const val TAG = "LocationObserver"
    }

    private val context = serviceContext

    private var locationManager: LocationManager? = null
    private var myLocationListener: LocationListener? = null

    override fun onCreate(owner: LifecycleOwner) {
        super.onCreate(owner)
        startLocation()
    }

    override fun onDestroy(owner: LifecycleOwner) {
        super.onDestroy(owner)
        stopLocation()
    }

    @SuppressLint("MissingPermission")
    private fun startLocation() {
        Log.e(TAG, "startLocation: ", )
        locationManager = context.getSystemService(Context.LOCATION_SERVICE) as LocationManager
        myLocationListener = MyLocationListener()
        myLocationListener?.let {
            locationManager?.requestLocationUpdates(
                LocationManager.GPS_PROVIDER,
                3000,//每三秒获取一次
                10f,//每移动10米获取一次
                it
            )
        }
    }
    
    private fun stopLocation() {
        myLocationListener?.let {
            locationManager?.removeUpdates(it)
        }
    }

    private class MyLocationListener : LocationListener {

        companion object {
            private const val TAG = "LocationObserver"
        }

        override fun onLocationChanged(location: Location) {
            Log.e(TAG, "onLocationChanged: $location")
        }

    }

}
```

自定义Service继承`LifecycleService`

```kotlin
class LocationLifecycleService: LifecycleService() {
    companion object {
        private const val TAG = "LocationLifecycleService"
    }

    init {
        Log.e(TAG, "LocationLifecycleService init ")
        val locationObserver = LocationObserver( this)
        lifecycle.addObserver(locationObserver)
    }
}
```

Activity:

```kotlin
class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
        initClick()
    }

    private fun initClick() {
        binding.start.setOnClickListener{
            startService(Intent(this@MainActivity,LocationLifecycleService::class.java))
        }

        binding.stop.setOnClickListener{
            stopService(Intent(this@MainActivity,LocationLifecycleService::class.java))
        }
    }
}
```

在AndroidManifest.xml中添加权限和注册Service

```xml
   <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
   <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
   
   <application
        android:allowBackup="true">
        <service android:name=".LocationLifecycleService" />
    </application>
```



## 使用ProcesslifecycleOwner 监听应用程序生命周期

* 针对整个应用程序的监听，与Activity数量无关
* Lifecycle.Event.ON_CREATE只会被调用一次，Lifecycle.Event.ON_DESTROY永远不会被调用

添加依赖:

```groovy
implementation 'androidx.lifecycle:lifecycle-process:2.6.0-alpha01'
```

```kotlin
class ApplicationObserver: LifecycleEventObserver {
    companion object{
        private const val TAG = "ApplicationObserver"
    }
    override fun onStateChanged(source: LifecycleOwner, event: Lifecycle.Event) {
        when(event){
            Lifecycle.Event.ON_CREATE -> Log.e(TAG, "onStateChanged: ON_CREATE", )
            Lifecycle.Event.ON_START -> Log.e(TAG, "onStateChanged: ON_START", )
            Lifecycle.Event.ON_RESUME -> Log.e(TAG, "onStateChanged: ON_RESUME", )
            Lifecycle.Event.ON_PAUSE -> Log.e(TAG, "onStateChanged: ON_PAUSE", )
            Lifecycle.Event.ON_STOP -> Log.e(TAG, "onStateChanged: ON_STOP", )
            Lifecycle.Event.ON_DESTROY -> Log.e(TAG, "onStateChanged: ON_DESTROY", )
            Lifecycle.Event.ON_ANY -> Log.e(TAG, "onStateChanged: ")
        }

    }
}
```

Application中使用

```kotlin
class MyApplication : Application() {

    override fun onCreate() {
        super.onCreate()

        ProcessLifecycleOwner.get().lifecycle.addObserver(ApplicationObserver())
    }
}
```



## 应用场景:

  ### 应用启动广告

```kotlin
class AdvertisingManage: LifecycleEventObserver{
    companion object{
        private const val TAG = "AdvertisingManage"
    }

    var advertisingManagerListener: AdvertisingManagerListener? = null

    private var countDownTimer: CountDownTimer? = object : CountDownTimer(5000,1000){
        override fun onTick(p0: Long) {
            Log.e(TAG, "广告剩余${(p0 / 1000).toInt()}秒"  )
            advertisingManagerListener?.timing((p0 / 1000).toInt())
        }

        override fun onFinish() {
            Log.e(TAG, "广告结束,准备进入主界面" )
            advertisingManagerListener?.enterMainActivity()
        }

    }

    private fun start(){
        Log.e(TAG, "开始计时" )
        countDownTimer?.start()
    }

    private fun stop(){
        Log.e(TAG, "停止计时", )
        countDownTimer?.cancel()
        countDownTimer = null
    }


    interface AdvertisingManagerListener {

        fun timing(second: Int)

        fun enterMainActivity()
    }

    override fun onStateChanged(source: LifecycleOwner, event: Lifecycle.Event) {
        when(event){
            Lifecycle.Event.ON_CREATE -> start()
            Lifecycle.Event.ON_DESTROY -> stop()
            else -> {}
        }
    }
}
```



```kotlin
class AdvertisingActivity : AppCompatActivity() {

    private lateinit var binding: ActivityAdvertisingBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = ActivityAdvertisingBinding.inflate(layoutInflater)

        setContentView(binding.root)

        val advertisingManage = AdvertisingManage()
        advertisingManage.advertisingManagerListener = object : AdvertisingManage.AdvertisingManagerListener{
            @SuppressLint("SetTextI18n")
            override fun timing(second: Int) {
                binding.textView.apply {
                    text = "广告剩余${second}秒"
                }
            }
            override fun enterMainActivity() {
                startActivity(Intent(this@AdvertisingActivity,MainActivity::class.java))
            }
        }
        binding.button.apply {
            setOnClickListener{
                startActivity(Intent(this@AdvertisingActivity,MainActivity::class.java))
                finish()
            }
        }
        //在Activity注册Oberver
        lifecycle.addObserver(advertisingManage)
    }

}
```



### 打造一个防止内存泄漏的Dialog

```kotlin
class TipDialog(context: Context) : Dialog(context),LifecycleObserver{

    init {
        if (context is ComponentActivity){
            context.lifecycle.addObserver(this)
        }
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.dialog_tip)
    }

    @OnLifecycleEvent(Lifecycle.Event.ON_DESTROY)
    private fun onDestroy(){
        if (isShowing){
            dismiss()
        }
    }
}
```

