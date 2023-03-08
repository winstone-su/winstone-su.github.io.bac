

# Hexo - 部署到Github

### 连接到Github

### 配置git用户名和密码

```shell
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

### 生成SSH Key

```shell
ssh-keygen -t rsa -C "邮箱"
```
SSH Key的位置:

> Windows下： C/Users/Administrator/.ssh/id_ras.pub
>
> MacOS:   ~/.ssh/id_ras.pub

### 在Github添加SSH

![image-20230308142938324](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303081429408.png)

### 验证SSH配置是否成功

```shell
ssh -T git@github.com
```

如果成功会提示:

```shell
Hi XXX! You've successfully authenticated, but GitHub does not provide shell access.
```

## Github创建同名仓库

在github上创建一个和用户名相同的仓库，以`.github.io`结尾，`<用户名>.github.io`

![image-20230308143413677](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303081434716.png)

## Hexo配置

### 添加依赖

为了正常部署到github仓库，需要先安装`hexo-deployer-git`插件。在Hexo根目录输入

```shell
npm install hexo-deployer-git --save
```

如果没有安装的话会报错

```shell
INFO Validating config
ERROR Deployer not found: git
```

### 修改配置文件

修改Hexo根目录的`_config.xml`文件，修改`deploy`的内容：

```yaml
deploy:
  type: git
  # 这里填写自己的github的名称即可
  repository: ssh://git@github.com/用户名/用户名.github.io.git
  # 注意这里，检查github的默认分支是 main 还是 master
  brandh: main
  messge:
```

## 部署到远程仓库

每次重新开一个新的终端都要重新连接git：

```shell
ssh -T git@github.com
```

执行下面的命令，然后再次进入Pages的链接`https://用户名.github.io`就可以看到你的博客了。

```powershell
hexo generate
hexo deploy
```

效果如下：

![image-20230308144300442](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303081443490.png)
