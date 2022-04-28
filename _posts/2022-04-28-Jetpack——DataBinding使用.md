



### RecyclerView的绑定

效果图：

![image](https://raw.githubusercontent.com/winstone-su/imageHosting/main/img/dataBindingRecyclerView.jpg)



列表适配器:

```java
public class DisplayAdapter extends RecyclerView.Adapter<DisplayAdapter.DisplayViewHolder> {
    List<User> users;
    public DisplayAdapter(List<User> users) {
        this.users = users;
    }
    @NonNull
    @Override
    public DisplayViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
      //创建ViewHolder时,传入对应的 XXXBinding
         ItemDisplayBinding binding = DataBindingUtil.inflate(LayoutInflater.from(parent.getContext()),
                R.layout.item_display,
                parent,
                false);
        return new DisplayViewHolder(binding);
    }
    @Override
    public void onBindViewHolder(@NonNull DisplayViewHolder holder, int position) {
        User user = users.get(position);
        holder.itemDisplayBinding.setUser(user);
    }
    @Override
    public int getItemCount() {
        return users.size();
    }
  
    static class DisplayViewHolder extends RecyclerView.ViewHolder{
        private final ItemDisplayBinding itemDisplayBinding;
        //构造方法传入binding
        public DisplayViewHolder(ItemDisplayBinding binding) {
            super(binding.getRoot());
            this.itemDisplayBinding = binding;
        }
    }
}
```

XML：

```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="user"
            type="com.carl.demo.databinding.User" />
    </data>
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">
        <!--app:itemImage 自定义的bindingAdapter-->
        <ImageView
            android:id="@+id/imageView"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_marginStart="40dp"
            app:itemImage="@{user.image}"
            android:layout_marginTop="20dp"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            tools:srcCompat="@tools:sample/backgrounds/scenic"
            android:contentDescription="@string/app_name" />

        <TextView
            android:id="@+id/userName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="32dp"
            android:layout_marginTop="20dp"
            android:text="@{user.userName}"
            android:textSize="24sp"
            app:layout_constraintStart_toEndOf="@+id/imageView"
            app:layout_constraintTop_toTopOf="parent" />

        <TextView
            android:id="@+id/desc"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginStart="32dp"
            android:text="@{user.desc}"
            android:textSize="18sp"
            app:layout_constraintBottom_toBottomOf="@+id/imageView"
            app:layout_constraintStart_toEndOf="@+id/imageView" />
    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

ImageView的视图绑定:

```java
public class DisplayBindingAdapter {
		//这里注意要用static，不然运行时会报错
    @BindingAdapter("itemImage")
    public static void setImageView(ImageView imageView,String image){
        if (!TextUtils.isEmpty(image)){
            Glide.with(imageView).load(image).into(imageView);
        }
    }
}
```

***视图绑定方法要用static修饰***





