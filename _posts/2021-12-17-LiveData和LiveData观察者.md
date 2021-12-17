---
layout: post

title: LiveData和LiveData观察者

categories: Kotlin

description: 

keywords: Android,Kotlin,LiveData

topmost: false


---

## 1.Add LiveData to ViewModel 

​	Add LiveData to ViewModel and encapsulate the LiveData

```kotlin
    // The current word
    private val _word = MutableLiveData<String>()
    val word: LiveData<String>
        get() = _word

    // The current score
    private val _score = MutableLiveData<Int>()
    val score: LiveData<Int>
        get() = _score
```

## 2.Attach observers to the LiveData objects

在`Activity`中使用:

```kotlin
 viewModel.score.observe(this, Observer { newScore ->
            Log.e(TAG, "$newScore" )
        })
```

在`Fragment`中使用:

```kotlin
viewModel.score.observe(viewLifecycleOwner, Observer { newScore ->
            binding.scoreText.text = newScore.toString()
        })
```

```shell
Why use viewLifecycleOwner?
Fragment views get destroyed when a user navigates away from a fragment, even though the fragment itself is not destroyed. This essentially creates two lifecycles, the lifecycle of the fragment, and the lifecycle of the fragment's view. Referring to the fragment's lifecycle instead of the fragment view's lifecycle can cause subtle bugs when updating the fragment's view. Therefore, when setting up observers that affect the fragment's view you should:

1. Set up the observers in onCreateView()

2. Pass in viewLifecycleOwner to observers
```



