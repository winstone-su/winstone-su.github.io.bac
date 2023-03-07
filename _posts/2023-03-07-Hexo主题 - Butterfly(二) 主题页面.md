

# Hexo主题 - Butterfly(二) 主题页面

## Front-matter

**Front-matter** 是 **markdown** 文件最上方以 <font color='red'> --- </font> 分隔的区域，用于指定个别档案的变数。

Page Front-matter 用于<font color='red'>页面</font> 配置
Post Front-matter 用于<font color='red'>文章页</font> 配置

> 如果标注<font color='red'>可选</font>的参数，可根据自己需要添加，不用全部都写在markdown里

### Page Front-matter

```markdown
---
title:
date:
updated:
type:
comments:
description:
keywords:
top_img:
mathjax:
katex:
aside:
aplayer:
highlight_shrink:
---
```

|       写法       | 解释                                                         |
| :--------------: | :----------------------------------------------------------- |
|      title       | 【必需】页面标题                                             |
|       date       | 【必需】页面创建日期                                         |
|       type       | 【必需】标签、分类和友情链接三个页面需要配置                 |
|     updated      | 【可选】页面更新日期                                         |
|   description    | 【可选】页面描述                                             |
|     keywords     | 【可选】页面关键字                                           |
|     comments     | 【可选】显示页面评论模块(默认 true)                          |
|     top_img      | 【可选】页面顶部图片                                         |
|     mathjax      | 【可选】显示mathjax(当设置mathjax的per_page: false时，才需要配置，默认 false) |
|      katex       | 【可选】显示katex(当设置katex的per_page: false时，才需要配置，默认 false) |
|      aside       | 【可选】显示侧边栏 (默认 true)                               |
|     aplayer      | 【可选】在需要的页面加载aplayer的js和css,请参考文章下面的<font color='red'>音乐</font> 配置 |
| highlight_shrink | 【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置) |

### Post Front-matter

```markdown
---
title:
date:
updated:
tags:
categories:
keywords:
description:
top_img:
comments:
cover:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
```

| 写法                  | 解释                                                         |
| --------------------- | ------------------------------------------------------------ |
| title                 | 【必需】文章标题                                             |
| date                  | 【必需】文章创建日期                                         |
| updated               | 【可选】文章更新日期                                         |
| tags                  | 【可选】文章标签                                             |
| categories            | 【可选】文章分类                                             |
| keywords              | 【可选】文章关键字                                           |
| description           | 【可选】文章描述                                             |
| top_img               | 【可选】文章顶部图片                                         |
| cover                 | 【可选】文章缩略图(如果没有设置top_img,文章页顶部将显示缩略图，可设为false/图片地址/留空) |
| comments              | 【可选】显示文章评论模块(默认 true)                          |
| toc                   | 【可选】显示文章TOC(默认为设置中toc的enable配置)             |
| toc_number            | 【可选】显示toc_number(默认为设置中toc的number配置)          |
| toc_style_simple      | 【可选】显示 toc 简洁模式                                    |
| copyright             | 【可选】显示文章版权模块(默认为设置中post_copyright的enable配置) |
| copyright_author      | 【可选】文章版权模块的<font color='red'>文章作者</font>      |
| copyright_author_href | 【可选】文章版权模块的<font color='red'>文章作者</font>链接  |
| copyright_url         | 【可选】文章版权模块的<font color='red'>文章连结</font>链接  |
| copyright_info        | 【可选】文章版权模块的<font color='red'>版权说明</font>文字  |
| mathjax               | 【可选】显示mathjax(当设置mathjax的per_page: false时，才需要配置，默认 false) |
| katex                 | 【可选】显示katex(当设置katex的per_page: false时，才需要配置，默认 false) |
| aplayer               | 【可选】在需要的页面加载aplayer的js和css,请参考文章下面的<font color='red'>音乐</font> 配置 |
| highlight_shrink      | 【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置) |
| aside                 | 【可选】显示侧边栏 (默认 true)                               |

## 标签页

1. 前往你的 Hexo 博客的根目录

2. 输入<font color='red'>`hexo new page tags`</font>

3. 找到<font color='red'>`source/tags/index.md`</font>这个文件

4. 修改这个文件：

   *记得添加* <font color='red'>`type: "tags"`</font>

```markdown
title: 标签
type: "tags"
date: 2023-03-07 14:37:20
orderby: random
order: 1
```

| 参数    | 解释                                                         |
| ------- | ------------------------------------------------------------ |
| type    | 【必须】页面类型，必须为<font color= "red">`tags`</font>     |
| orderby | 【可选】排序方式 ：random/name/length                        |
| order   | 【可选】排序次序： 1, asc for ascending; -1, desc for descending |

## 分类页

1. 前往 Hexo 博客的根目录

2. 输入<font color="red">`hexo new page categories`</font>

3. 找到<font color="red">`source/categories/index.md`</font>这个文件

4. 修改这个文件：

   *记得添加* <font color='red'>`type: "categories"`</font>

```mark
---
title: 分类
type: "categories"
date: 2023-03-07 14:49:03
---
```

## 友情链接

为你的博客创建一个友情链接！

### 创建友情链接页面

1. 前往 Hexo 博客的根目录

2. 输入 <font color="red">`hexo new page link`</font>

3. 找到<font color="red">`source/link/index.md`</font>这个文件

4. 修改这个文件：

   *记得添加* <font color='red'>`type: "link"`</font>

### 友情链接添加

#### 本地生成

在Hexo博客目录中的<font color="red">`source/_data`</font>（如果没有 _data 文件夹，请自行创建），创建一个文件<font color="red">`link.yml`</font>

```yaml
- class_name: 友情链接
  class_desc: 那些人，那些事
  link_list:
    - name: Hexo
      link: https://hexo.io/zh-tw/
      avatar: https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg
      descr: 快速、简单且强大的网志框架

- class_name: 网站
  class_desc: 值得推荐的网站
  link_list:
    - name: Youtube
      link: https://www.youtube.com/
      avatar: https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png
      descr: 视频网站
    - name: Weibo
      link: https://www.weibo.com/
      avatar: https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png
      descr: 中国最大社交分享平台
    - name: Twitter
      link: https://twitter.com/
      avatar: https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png
      descr: 社交分享平台
```

<font color="red">`class_name`</font> 和<font color="red">` class_desc`</font> 支持 html 格式书写，如不需要，也可以留空。

#### 远程拉取

从 <font color="red">`4.0.0`</font>开始，支持从远程加载友情链接，远程拉取只支持 <font color="red">`json`</font>。

注意： 选择远程加载后，本地生成的方法会无效。

在<font color="red">`source/link/index.md`</font> 这个文件的 front-matter 添加远程链接

```markdown
flink_url: xxxxx
```

Json 的格式

```json
[
  {
    "class_name": "友情链接",
    "class_desc": "那些人，那些事",
    "link_list": [
      {
        "name": "Hexo",
        "link": "https://hexo.io/zh-tw/",
        "avatar": "https://d33wubrfki0l68.cloudfront.net/6657ba50e702d84afb32fe846bed54fba1a77add/827ae/logo.svg",
        "descr": "快速、简单且强大的网志框架"
      }
    ]
  },
  {
    "class_name": "网站",
    "class_desc": "值得推荐的网站",
    "link_list": [
      {
        "name": "Youtube",
        "link": "https://www.youtube.com/",
        "avatar": "https://i.loli.net/2020/05/14/9ZkGg8v3azHJfM1.png",
        "descr": "视频网站"
      },
      {
        "name": "Weibo",
        "link": "https://www.weibo.com/",
        "avatar": "https://i.loli.net/2020/05/14/TLJBum386vcnI1P.png",
        "descr": "中国最大社交分享平台"
      },
      {
        "name": "Twitter",
        "link": "https://twitter.com/",
        "avatar": "https://i.loli.net/2020/05/14/5VyHPQqR6LWF39a.png",
        "descr": "社交分享平台"
      }
    ]
  }
]
```

### 友情链接界面设置

由 2.2.0 起，友情链接界面可以由用户自己自定义，只需要在友情链接的md档设置就行，以普通的Markdown格式书写。

## 图库

图库页面只是普通的页面，你只需要<font color="red">`hexo n page xxxxx `</font>创建你的页面就行

然后使用标签外挂 [galleryGroup](https://butterfly.js.org/posts/4aa8abbe/#Gallery%E7%9B%B8%E5%86%8A%E5%9C%96%E5%BA%AB)，具体用法请查看对应的内容。

```yaml
<div class="gallery-group-main">
{% galleryGroup '壁纸' '收藏的一些壁纸' '/Gallery/wallpaper' https://i.loli.net/2019/11/10/T7Mu8Aod3egmC4Q.png %}
{% galleryGroup '漫威' '关于漫威的图片' '/Gallery/marvel' https://i.loli.net/2019/12/25/8t97aVlp4hgyBGu.jpg %}
{% galleryGroup 'OH MY GIRL' '关于OH MY GIRL的图片' '/Gallery/ohmygirl' https://i.loli.net/2019/12/25/hOqbQ3BIwa6KWpo.jpg %}
</div>
```

<div class="gallery-group-main">
{% galleryGroup '壁纸' '收藏的一些壁纸' '/Gallery/wallpaper' https://i.loli.net/2019/11/10/T7Mu8Aod3egmC4Q.png %}
{% galleryGroup '漫威' '关于漫威的图片' '/Gallery/marvel' https://i.loli.net/2019/12/25/8t97aVlp4hgyBGu.jpg %}
{% galleryGroup 'OH MY GIRL' '关于OH MY GIRL的图片' '/Gallery/ohmygirl' https://i.loli.net/2019/12/25/hOqbQ3BIwa6KWpo.jpg %}
</div>



### 子页面

子页面也是普通的页面，你只需要<font color ="red">`hexo n page xxxxx`</font> 创建你的页面就行

然后使用标签外挂 [gallery](https://butterfly.js.org/posts/4aa8abbe/#Gallery%E7%9B%B8%E5%86%8A)，具体用法请查看对应的内容。

```yaml
{% gallery %}
![](https://i.loli.net/2019/12/25/Fze9jchtnyJXMHN.jpg)
![](https://i.loli.net/2019/12/25/ryLVePaqkYm4TEK.jpg)
![](https://i.loli.net/2019/12/25/gEy5Zc1Ai6VuO4N.jpg)
![](https://i.loli.net/2019/12/25/d6QHbytlSYO4FBG.jpg)
![](https://i.loli.net/2019/12/25/6nepIJ1xTgufatZ.jpg)
![](https://i.loli.net/2019/12/25/E7Jvr4eIPwUNmzq.jpg)
![](https://i.loli.net/2019/12/25/mh19anwBSWIkGlH.jpg)
![](https://i.loli.net/2019/12/25/2tu9JC8ewpBFagv.jpg)
{% endgallery %}
```

有关图库和子页面的详细设置可以参考

`https://butterfly.js.org/posts/dc584b87/#%E5%9C%96%E5%BA%AB` 和`https://butterfly.js.org/posts/4aa8abbe/#Gallery%E7%9B%B8%E5%86%8A%E5%9C%96%E5%BA%AB`

> 如果你想要使用 /photo/ohmygirl 这样的链接显示你的图片内容
>
> 你可以把创建好的 ohmygirl整个文件夹移到 photo文件夹里去

## 404页面

主题内置了一个简单的404页面，可在设置中开启

> 本地预览时，访问出错的网站是不会跳到404页面的。
>
> 如需本地预览，请访问http://localhost:4000/404.html

```yaml
# A simple 404 page
error_404:
  enable: true
  subtitle: "页面没有找到"
  background: https://i.loli.net/2020/05/19/aKOcLiyPl2JQdFD.png
```

