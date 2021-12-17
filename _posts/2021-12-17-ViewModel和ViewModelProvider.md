---
layout: post

title: ViewModel和ViewModelProvider

categories: Kotlin

description: 

keywords: Android,Kotlin,ViewModel,ViewModelProvider

topmost: false



---

## 依赖

```shell
//ViewModel
implementation 'androidx.lifecycle:lifecycle-viewmodel-ktx:2.2.0'
```

## 创建ViewModel

```kotlin
class GameViewModel : ViewModel() {
   init {
       Log.i("GameViewModel", "GameViewModel created!")
   }
}
```

## 关联并初始化

### 声明

```kotlin
private lateinit var viewModel: GameViewModel
```

### 初始化

```kotlin
viewModel = ViewModelProvider(this).get(GameViewModel::class.java)
```

```xml
Important: Always use ViewModelProvider to create ViewModel objects rather than directly instantiating an instance of ViewModel.
```

## 使用ViewModelFactory

```kotlin
class ScoreViewModel(finalScore: Int) : ViewModel() {
   // The final score
   var score = finalScore
   init {
       Log.i("ScoreViewModel", "Final score is $finalScore")
   }
}
```

```kotlin
class ScoreViewModelFactory(private val finalScore: Int) : ViewModelProvider.Factory {
    override fun <T : ViewModel?> create(modelClass: Class<T>): T {
        if (modelClass.isAssignableFrom(ScoreViewModel::class.java)) {
            return ScoreViewModel(finalScore) as T
        }
        throw IllegalArgumentException("Unknown ViewModel class")
    }
}

```

