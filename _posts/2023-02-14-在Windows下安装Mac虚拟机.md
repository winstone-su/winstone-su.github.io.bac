

# 在Windows下安装Mac虚拟机



## 开启虚拟化

**步骤：关机 --> 重启 --> 进入BIOS界面 --> 开启虚拟化 **

具体是AMD的还是Intel的CPU，请自行查阅文档设置.

设置完成后，可以在**任务管理器 -- 性能 -- CPU**里面查看虚拟化是否开启

<img src="http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141420768.png" style="zoom: 80%;" />

***同时禁用`Hyper-V`和`Credential Guard`。***

## MacOS镜像下载

镜像可以自行从苹果官网下载

已经上传12.2的系统至阿里网盘

## 安装VMware虚拟机

已上传至阿里网盘，可自行激活

```SAS
VMwareworkstation16.0.0 https://www.aliyundrive.com/s/9uDsraHjsoB 提取码: 40oe 点击链接保存，或者复制本段内容，打开「阿里云盘」APP ，无需下载极速在线查看，视频原画倍速播放。
```

## 创建MacOS虚拟机

打开`VMware Workstation`，在选项卡`文件`,`新建虚拟机`

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141429015.png)

选择刚才下载的iso镜像文件

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141430945.png)

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141430289.png)

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141431689.png)

如果没有解锁过VMware，选择操作系统的时候是不会看到`Apple Mac OS X(M)`这个选项的。

这里我们用到一个github上的解锁神器`auto-unlocker`

https://github.com/paolo-projects/auto-unlocker/releases

打开之后，只有一个exe文件，点击执行。

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141435614.png)

如果打开了类似模拟器相关的程序，先关闭，否则可能出现异常。点击`Patch`

等待下载文件，自动执行。*如果没有执行成功，多执行几次*。

执行成功后，重复执行之前的步骤，就可以看到MacOS的选项了。

***然后修改虚拟机设置，修改内存为8G或者以上，CPU内核修改为4以上***

启动虚拟机，安装系统。

## 安装VMware Tools

安装系统完以后，会发现系统非常卡顿，这是因为显卡内存只有3M。

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141444566.png)

如果这里可以安装VMware Tools,那么可以直接安装。

如果不能安装的话，需要手动选择iso文件。

打开虚拟机设置，在`CD/DVD`选项里选择ISO镜像文件

<img src="http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141446463.png" style="zoom:67%;" />

在VMware的安装目录下找到`darwin.iso`文件

`我的VMware安装目录是：  D:\Program Files (x86)\VMware\VMware Workstation`

然后，重启系统，在桌面可以看到`VMWare Tools`的安装程序

这里会弹出`系统扩展已被阻止`的弹框，在`安全偏好设置`里面允许即可。

安装完成后，重启虚拟机，可以看到显卡的容量已经变为 `128MB`

![](http://rpheez113.hn-bkt.clouddn.com/course/kotlin/kotlin-first-lesson/image/202302141449408.png)