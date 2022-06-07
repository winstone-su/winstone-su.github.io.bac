



***模拟场景： 在Activity定义两个相同的Fragment，等分布局，Fragment里面只包含一个SeekBar控件，通过共享ViewModel来实现Fragment间的通讯***

### 1. 定义ViewModel和LiveData

```kotlin
class SharedViewModel: ViewModel() {
    val progress: MutableLiveData<Int> = MutableLiveData()
}
```

### 2. 布局文件

activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/fragmentContainerView"
        android:name="com.carl.demo.viewmodeldemo.TopFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"/>
    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/fragmentContainerView3"
        android:name="com.carl.demo.viewmodeldemo.CenterFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"/>
</LinearLayout>
```

fragment_top.xml(fragment_bottom.xml相同)

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".TopFragment">
    <SeekBar
        android:layout_gravity="center"
        android:id="@+id/seekBar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</FrameLayout>
```

### 3.Fragment文件

如果使用的是Kotlin，那么在依赖中声明：

```groovy
implementation 'androidx.activity:activity-ktx:1.6.0-alpha04'  //在Activity中使用 by viewModels()
implementation 'androidx.fragment:fragment-ktx:1.5.0-rc01'   //在Fragment中使用 by activityViewModels()
```

声明 sharedViewModel

Kotlin:

```kotlin
val sharedViewModel: SharedViewModel by activityViewModels() 
```

Java:

```java
private SharedViewModel sharedViewModel;
sharedViewModel = new ViewModelProvider(this.requireActivity()).get(SharedViewModel.class);
```



监听和改变liveData

Kotlin:

```kotlin
val liveData = sharedViewModel.progress
liveData.observe(viewLifecycleOwner){ progress ->
    binding.seekBar.progress = progress
}

binding.seekBar.setOnSeekBarChangeListener(object : SeekBar.OnSeekBarChangeListener{
    override fun onProgressChanged(seekBar: SeekBar?, progress: Int, fromUser: Boolean) {
				liveData.value = progress
    }
    override fun onStartTrackingTouch(seekBar: SeekBar?) {
    }

    override fun onStopTrackingTouch(seekBar: SeekBar?) {
    }

})
```

Java:

```java
 MutableLiveData<Integer> progressLiveData = sharedViewModel.getProgress();

progressLiveData.observe(getViewLifecycleOwner(), integer -> binding.seekBar.setProgress(integer));

binding.seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
    @Override
    public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
				progressLiveData.setValue(progress);
    }
    @Override
    public void onStartTrackingTouch(SeekBar seekBar) {
    }
    @Override
    public void onStopTrackingTouch(SeekBar seekBar) {
    }
});
```



最终效果： 拖动任意seekbar，另外一个seekbar也会随之变化