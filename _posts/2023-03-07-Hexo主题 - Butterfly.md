

# Hexo主题 - Butterfly(一)--快速开始

## 安装

### Github

在Hexo根目录

稳定版

```powershell
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

> 升级方法：在主题目录下，运行 `git pull`

### npm安装

> 此方法只支持 Hexo 5.0.0 以上版本
>
> 通过npm安装不会在themes里生成主题文件夹，而是在`node_modules`里生成。

在Hexo根目录

```powershell
npm i hexo-theme-butterfly
```

> 升级方法：在Hexo根目录下，运行 npm update hexo-theme-butterfly

## 应用主题

修改Hexo根目录下的 `_config.yml`，把主题改为`butterfly`

```yaml
theme: butterfly
```

## 安装插件

如果你没有pug以及stylus的渲染器，需要安装:

```powershell
npm install hexo-renderer-pug hexo-renderer-stylus --save
```

## 升级建议

> 升级完成后，请到Github的 Releases 界面查看新版的更新内容。 
>
> 里面有标注 _config 文件的变更内容，请根据实际情况更新你的配置内容。

为了减少升级主题带来的不便，请使用以下方法(建议，可以不做)。

在hexo的根目录下创建一个文件 `_config.butterfly.yml`，并把主题目录的`_config.yml`内容复制到`_config.butterfly.yml`去（注意：复制的是主题下的`_config.yml`，而不是hexo的`_config.yml`）

> `注意： 不要把主題目錄的 _config.yml 刪掉`

> 注意： 以后只需要在`_config.butterfly.yml`进行配置就行。
>
> 如果使用了`_config.butterfly.yml`配置主题的`_config.yml`将不会有效果。

Hexo会自动合并主题中的`_config.yml`和`_config.butterfly.yml`里的配置。如果存在同名配置，会使用`_config.butterfly.yml`的配置，其优先级较高。

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071151281.png)



更多设置：参考[butterfly官网](https://butterfly.js.org/page/2/#content-inner)







