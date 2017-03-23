---
layout: post
title: "利用github作iOS企业分发App"
date: 2014-11-12 16:00:00
description: "利用github作iOS企业分发App"
tag: iOS

---


iOS7.0以后安装企业分发App需要HTTPS证书，如果网站没有CA受信用的HTTPS证书,可以利用github来实现。

首先在Github上面新建一个Repository,然后把已经制作好的Plist文件上传上去,点开plist找到Raw

![img](http://img.blog.csdn.net/20141112155413099?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VfaG9tZQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast "carl")

看到别人用七牛([http://www.qiniu.com][href-qiniu])也可以实现企业分发,不过这个网站需要上传身份证正反照片,手上暂时没有,下次再做测试。

[href-qiniu]: http://www.qiniu.com