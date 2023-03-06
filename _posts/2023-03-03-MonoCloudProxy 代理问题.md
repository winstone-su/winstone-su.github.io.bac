

# MonoCloudProxy 代理问题

## 问题场景

在配置Flutter安装环境时，运行`flutter doctor`时，有这个错误

```shell
   X HTTP host "https://maven.google.com/" is not reachable. Reason: An error occurred while checking the HTTP host:
      信号灯超时时间已到

    X HTTP host "https://pub.dev/" is not reachable. Reason: An error occurred while checking the HTTP host: 信号灯超时 时间已到

    X HTTP host "https://cloud.google.com/" is not reachable. Reason: An error occurred while checking the HTTP host:
      信号灯超时时间已到
```

原因是无法访问外网的服务器，直接打开MonoCloud，发现还是一样的结果

在Windows下：

使用 MonoCloud 客户端，打开代理设置。

发现打开PowerShell,还是无法访问外网。

```shell
 netsh winhttp show proxy
```

查看代理网络设置，这是可以看到，代理是通过`127.0.0.1:8888`这个端口发出去

## 取消代理

```shell
netsh winhttp reset proxy
```

然后重新运行`flutter doctor `，结果正常