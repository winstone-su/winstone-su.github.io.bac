---
layout: post

title: Postman截取Chrome网络请求

categories: Postman

description: 

keywords: Postman

topmost: true




---

# 1.安装Chrome插件

## 安装 `Postman Interceptor` 插件

[ https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo?hl=zh]( https://chrome.google.com/webstore/detail/postman-interceptor/aicmkgpgakddgnaphhhpliifpcfhicfo?hl=zh)

# 2.安装 `Interceptor Bridge `

按照 [https://learning.postman.com/docs/sending-requests/capturing-request-data/interceptor/](https://learning.postman.com/docs/sending-requests/capturing-request-data/interceptor/) 设置安装



![Interceptor Bridge]({{site.url}}/assets/images/202106/20210625-1.png) 

 ```html
 Mac OS下需要先安装Node.js环境，没有的话，会自动下载node.js的安装包
 ```



# 打开Requests 和Cookies

​		![Request Cookie]({{site.url}}/assets/images/202106/20210625-2.png) 

在`Requests` 里面选择 `Source` 为`Interceptor`，打开`Capture Requests`，然后选择请求保存的位置

​		![Request Cookie]({{site.url}}/assets/images/202106/20210625-3.png) 

在`Cookies`里面，打开`Capture Cookie`，然后在`Domains`里面可以过滤信息

# 重复请求测试

 在Postman左侧找到已经抓取到的请求，然后添加到`Save Request`，将请求添加到`Collections`

​		![Request Cookie]({{site.url}}/assets/images/202106/20210625-4.png) 

点击` Run collection`

​		![Request Cookie]({{site.url}}/assets/images/202106/20210625-5.png) 

`Iterations` 表示执行的次数

`Delay` 表示延时

`Save Responses` 可以查看相应结果



