---
layout: post

title: Data binding with ViewModel and LiveData

categories: Kotlin

description: 

keywords: Android,Kotlin,DataBinding

topmost: false




---

## 官方Demo

[https://developer.android.com/codelabs/kotlin-android-training-live-data-data-binding#0](https://developer.android.com/codelabs/kotlin-android-training-live-data-data-binding#0)

本文基于 ViewModel + LiveData 改造

## Gradle配置

```shell
android {
    buildFeatures {
        dataBinding true
    }
}
```

## Add ViewModel data binding

```xml
<layout ...>
   <data>
       <variable
           name="scoreViewModel"
           type="com.example.android.guesstheword.screens.score.ScoreViewModel" />
   </data>
   <androidx.constraintlayout.widget.ConstraintLayout
```

Button点击事件

```xml
<Button
   android:id="@+id/play_again_button"
   ...
   android:onClick="@{() -> scoreViewModel.onPlayAgain()}"
   ... />
```

Fragment中用`DataBindingUtil`初始化`binding`

```kotlin
override fun onCreateView(
            inflater: LayoutInflater,
            container: ViewGroup?,
            savedInstanceState: Bundle?
    ): View? {
        // Inflate view and obtain an instance of the binding class.
        val binding: ScoreFragmentBinding = DataBindingUtil.inflate(
                inflater,
                R.layout.score_fragment,
                container,
                false
        )
        return binding.root
    }
```

在Fragment中初始化`binding.scoreViewModel`

```kotlin
viewModelFactory = ScoreViewModelFactory(ScoreFragmentArgs.fromBundle(arguments!!).score)
viewModel = ViewModelProvider(this, viewModelFactory).get(ScoreViewModel::class.java)
//initial 
binding.scoreViewModel = viewModel
```

## Add LiveData to data binding

### XML配置

```xml
<TextView
   android:id="@+id/word_text"
   ...
   android:text="@{gameViewModel.word}"
   ... />
```

### Fragment修改

set the fragment view as the lifecycle owner of the `binding` variable

```kotlin
binding.gameViewModel = ...
// Specify the fragment view as the lifecycle owner of the binding.
// This is used so that the binding can observe LiveData updates
binding.lifecycleOwner = viewLifecycleOwner
```

### Add string formatting with data binding

### strings.xml

```xml
<string name="quote_format">\"%s\"</string>
<string name="score_format">Current Score: %d</string>
```

### layout.xml

```xml
<TextView
   android:id="@+id/word_text"
   ...
   android:text="@{@string/quote_format(gameViewModel.word)}"
   ... />
```

```xml
<TextView
   android:id="@+id/score_text"
   ...
   android:text="@{@string/score_format(gameViewModel.score)}"
   ... />
```

