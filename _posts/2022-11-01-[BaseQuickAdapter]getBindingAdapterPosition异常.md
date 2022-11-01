



# [BaseQuickAdapter]getBindingAdapterPosition异常



最近在使用`BaseRecyclerViewAdapterHelper`的时候，在设置adapter的`setOnItemClickListener`方法时，点击item报错

```shell
java.lang.NoSuchMethodError: No virtual method getBindingAdapterPosition()I in class Lcom/chad/library/adapter/base/viewholder/BaseViewHolder; or its super classes (declaration of 'com.chad.library.adapter.base.viewholder.BaseViewHolder' appears in /data/app/
```

问题原因是：

`getAdapterPosition`这个方法已经被废弃了，详见[https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.ViewHolder#getAdapterPosition()](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.ViewHolder#getAdapterPosition())

```sh
This method is deprecated.
This method is confusing when adapters nest other adapters. If you are calling this in the context of an Adapter, you probably want to call getBindingAdapterPosition or if you want the position as RecyclerView sees it, you should call getAbsoluteAdapterPosition.
```



解决办法：

  1.使用 不高于`com.github.CymChad:BaseRecyclerViewAdapterHelper:3.0.6`版本的库

2. 使用高于3.0.6版本的库，同时添加高于 `1.1.0`版本的recyclerview

```
implementation 'androidx.recyclerview:recyclerview:1.2.1'
```

