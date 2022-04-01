---
layout: post
title: Arcgis Runtime API for Android 100.13 (二)基本地图
categories: Arcgis for Android

description: 

keywords: Arcgis,Android

topmost: false

---

上篇介绍了环境配置，现在来展示一个基本二维地图

1、在`AndroidManifest.xml`中添加网络权限和OpenGL 2.0支持

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-feature
        android:glEsVersion="0x00020000"
        android:required="true" />
```

2、布局文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
    <com.esri.arcgisruntime.mapping.view.MapView
        android:id="@+id/mapView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</FrameLayout>
```

3、代码

```java
public class MainActivity extends AppCompatActivity {
    protected ActivityMainBinding binding;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        binding = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(binding.getRoot());
        setApiKeyForApp();
        setRequestConfiguration();
        setupMap();

    }

    private void setApiKeyForApp(){
        //设置Apikey和License
        ArcGISRuntimeEnvironment.setLicense("runtimelite,1000,rud9978704000,none,TRB3LNBHPFMB4P7EJ046");
        ArcGISRuntimeEnvironment.setApiKey("AAPK7bc88675e61a49f9bcb8ceb647c694f7wGb7zTAkJBYB8MWcOd3ale30A0sTU9dl8kr9uMEggfRfA3X9cNBrGXDIu3PwkIcp");
        //去除水印
        binding.mapView.setAttributionTextVisible(false);
    }

    private void setRequestConfiguration(){
        //设置RequestConfiguration
        RequestConfiguration requestConfiguration = new RequestConfiguration();
        requestConfiguration.getHeaders().put("referer", "http://www.arcgis.com");
        RequestConfiguration.setGlobalRequestConfiguration(requestConfiguration);
    }

    private void setupMap(){
        ArcGISMap map = new ArcGISMap(Basemap.Type.OPEN_STREET_MAP,27.822421448238604,111.98435756939104,13);
        binding.mapView.setMap(map);
    }

    @Override
    protected void onPause() {
        super.onPause();
        binding.mapView.pause();
    }

    @Override
    protected void onResume() {
        super.onResume();
        binding.mapView.resume();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        binding.mapView.dispose();
    }
}
```

效果如下:

![1](https://gitee.com/sliverfoxwb/image/raw/master/img/A3F0DA82-0D3B-4ad7-83C8-73CA7433698C.png)

