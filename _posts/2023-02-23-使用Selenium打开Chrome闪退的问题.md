

# 使用Selenium打开Chrome闪退的问题

## 检查驱动

http://chromedriver.storage.googleapis.com/index.html 下载驱动

`将chromedriver.exe放在python的安装目录下`

发现打开浏览器运行完程序后，浏览器会关闭

## 解决办法

```kotlin
url = 'https://www.baidu.com'
s = Service(r"C:\python\chromedriver.exe")
option = webdriver.ChromeOptions()
option.add_experimental_option('detach', True)
driver = webdriver.Chrome(service=s, options=option)
driver.get(url)
```

