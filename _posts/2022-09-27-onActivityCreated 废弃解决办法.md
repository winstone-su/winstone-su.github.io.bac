



# Fragment -- onActivityCreated 废弃解决办法



​	在新版SDK中，Fragment废弃了`onActivityCreated`方法，解决办法

在`onAttach()`方法中，使用lifecycle监听状态

```kotlin
override fun onAttach(context: Context) {
        super.onAttach(context)
        Log.e(TAG, "onAttach: ", )
        requireActivity().lifecycle.addObserver(object : LifecycleEventObserver {
            override fun onStateChanged(source: LifecycleOwner, event: Lifecycle.Event) {
                Log.e(TAG, "onStateChanged: " + event.targetState )
                if (event.targetState == Lifecycle.State.RESUMED){ //注意
                    viewModel = ViewModelProvider(this@HelpFragment)[MainViewModel::class.java]
                    viewModel.result.observe(viewLifecycleOwner) { result ->
                        binding.message.text = result
                    }
                    lifecycle.removeObserver(this)
                }
            }
        })
    }
```

这里需要注意的是，如果判断`event.targetState`的状态为`Lifecycle.State.CREATED`的话，里面就不能包含控件的引用

加了监听的生命周期为：

```kotlin
onAttach --> onCreate --> onStateChanged: CREATED --> onCreateView --> onActivityCreated -->  onStateChanged: STARTED --> onStateChanged: RESUMED
```

可以看到状态为`Lifecycle.State.CREATED`是在 onCrate之后，onCreateView之前，这个时候布局还没有完成