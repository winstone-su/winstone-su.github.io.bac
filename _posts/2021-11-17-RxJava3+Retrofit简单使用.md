---
layout: post

title: RxJava3+Retrofit简单使用

categories: Android

description: 

keywords: Android,RxJava3

topmost: false







---

## 

## 目标

​	从百度翻译定时轮询翻译API

### 依赖

```sh
		implementation 'io.reactivex.rxjava3:rxjava:3.1.2'
    implementation 'io.reactivex.rxjava3:rxandroid:3.0.0'
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'// 衔接 Retrofit & RxJava
    // retrofit适配器
    implementation 'com.squareup.retrofit2:adapter-rxjava3:2.9.0'
    // Gson解析
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```



### 权限:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

### https请求配置:

```xml
 <application
        android:usesCleartextTraffic="true">
 </application>
```

### 实体类

```java
@lombok.NoArgsConstructor
@lombok.Data
public class Translation {

    private String from;
    private String to;
    private List<TransResultBean> trans_result;

    @lombok.NoArgsConstructor
    @lombok.Data
    public static class TransResultBean {
        private String src;
        private String dst;
    }

    public void show(){
        Log.e("RxJava", trans_result.get(0).dst);
    }
}

```



### 描述网络请求接口

```java
public interface GetRequest_Interface {
    @GET("trans/vip/translate?q=apple&from=en&to=zh&appid=2015063000000001&salt=1435660288&sign=f89f9594663708c1605f3d736d01d2d4")
    Observable<Translation> getCall();
}
```

### 实现

```java
public class MainActivity extends AppCompatActivity {
    private static final String TAG = MainActivity.class.getSimpleName();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("http://api.fanyi.baidu.com/api/")
                .addConverterFactory(GsonConverterFactory.create())
                .addCallAdapterFactory(RxJava3CallAdapterFactory.create())
                .build();
        GetRequest_Interface request = retrofit.create(GetRequest_Interface.class);

        Observable.interval(3,5, TimeUnit.SECONDS)
                .doOnNext(aLong -> {
                    Log.e(TAG, "第 " + aLong + " 次轮询" );
                    Observable<Translation> observable = request.getCall();
                    observable.subscribeOn(Schedulers.io())
                            .observeOn(AndroidSchedulers.mainThread())
                            .subscribe(new Observer<Translation>() {
                                @Override
                                public void onSubscribe(@NonNull Disposable d) {

                                }

                                @Override
                                public void onNext(@NonNull Translation translation) {
                                    translation.show();
                                }

                                @Override
                                public void onError(@NonNull Throwable e) {
                                    Log.e(TAG, "onError: " );
                                }

                                @Override
                                public void onComplete() {

                                }
                            });
                }).subscribe(new Observer<Long>() {
            @Override
            public void onSubscribe(@NonNull Disposable d) {

            }

            @Override
            public void onNext(@NonNull Long aLong) {

            }

            @Override
            public void onError(@NonNull Throwable e) {
                e.printStackTrace();
                Log.e(TAG, "对Error事件作出响应");
            }

            @Override
            public void onComplete() {
                Log.e(TAG, "对Complete事件作出响应");
            }
        });
    }
}
```

