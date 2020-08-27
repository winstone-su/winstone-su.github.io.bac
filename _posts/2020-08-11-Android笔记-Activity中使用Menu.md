---
layout: post
title: Android-在Activity中使用Menu
categories: Android笔记
description: 
keywords: Android
topmost: false
---

# 在Activity中使用Menu

## 资源文件

​	首先在 `res` 目录下新建一个`menu`文件夹，右击`res`目录-->New-->Android Resource Directory，输入文件夹名`menu`，在弹出的菜单中`Directory Name`输入`Menu`，`Resource type` 选择`Menu`，然后在此文件夹下新建一个 `main.xml`的菜单文件，右击menu-->New-->Menu Resource File。

![img]({{site.url }}/assets/images/202008/0813-1.png)

![img]({{site.url }}/assets/images/202008/0813-2.png)

![img]({{site.url }}/assets/images/202008/0813-3.png)

最后添加 `Item`的 `id`和`title`即可.

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
<item
    android:id="@+id/add_item"
    android:title="@string/add" />
<item
    android:id="@+id/remove_item"
    android:title="@string/remove" />
</menu>
```



## 使用:

​	重写 `Activity`的 `onCreateOptionsMenu` 和 `onOptionsItemSelected` 方法.

```java
@Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main,menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()){
            case  R.id.add_item:
                showToast("You Click Add");
                break;
            case R.id.remove_item:
                showToast("You Click Remove");
                break;
            default:
        }
        return true;
    }
```



