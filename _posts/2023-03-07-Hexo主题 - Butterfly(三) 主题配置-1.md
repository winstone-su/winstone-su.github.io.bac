

# Hexo主题 - Butterfly(三) 主题配置-1

##  语言

修改站点配置文件<font color="red">` _config.yml`</font>

默认语言是 `en`

主题支持三种语言

- default(en)
- zh-CN (简体中文)
- zh-TW (繁体中文)

## 网站资料

修改网站各种资料，例如标题、副标题和邮箱等个人资料，请修改博客根目录的<font color="red">` _config.yml`</font>

![](https://file.crazywong.com/gh/jerryc127/CDN/img/20191120000444.png)

## 导航菜单

修改 <font color="red">`主题配置文件`</font>

> 注意: 如果我们前面配置了<font color="red">`_config.butterfly.yml`</font>，那么就修改根目录的<font color="red">`_config.butterfly.yml`</font>
>
> 如果没有配置<font color="red">`_config.butterfly.yml`</font>,就修改<font color="red">`node_modules\hexo-theme-butterfly\_config.xml`</font>

```yaml
Home: / || fas fa-home
Archives: /archives/ || fas fa-archive
Tags: /tags/ || fas fa-tags
Categories: /categories/ || fas fa-folder-open
List||fas fa-list:
  Music: /music/ || fas fa-music
  Movie: /movies/ || fas fa-video
Link: /link/ || fas fa-link
About: /about/ || fas fa-heart
```

必须是<font color="red">` /xxx/`</font>，后面<font color="red">` ||`</font>分开，然后写图标名。

如果不希望显示图标，图标名可不写。

默认子目录是展开的，如果你想要隐藏，在子目录里添加 <font color="red">` hide`</font>。

```yaml
List||fas fa-list||hide:
  Music: /music/ || fas fa-music
  Movie: /movies/ || fas fa-video
```

注意： 导航的文字可自行更改

例如：

```markdown
menu:
  首页: / || fas fa-home
  时间轴: /archives/ || fas fa-archive
  标签: /tags/ || fas fa-tags
  分类: /categories/ || fas fa-folder-open
  清单||fa fa-heartbeat:
    音乐: /music/ || fas fa-music
    照片: /Gallery/ || fas fa-images
    电影: /movies/ || fas fa-video
  友链: /link/ || fas fa-link
  关于: /about/ || fas fa-heart
```

<img src="https://file.crazywong.com/gh/jerryc127/CDN/img/hexo-theme-butterfly-doc-menu.png" style="zoom: 80%;" />

## 导航栏设置

主题配置文件中

```yaml
nav:
  logo: #image
  display_title: true
  fixed: false # fixed navigation bar
```

| 参数          | 解释                                    |
| ------------- | --------------------------------------- |
| logo          | 网站的 logo，支持图片，直接填入图片链接 |
| display_title | 是否显示网站标题，填写 true 或者 false  |
| fixed         | 是否固定状态栏，填写 true 或者 false    |

## 代码

> 代码块中的所有功能只适用于 Hexo 自带的代码渲染
>
> 如果使用第三方的渲染器，不一定会有效

### 代码高亮主题

{% tabs test1 %}
<!-- tab 默认主题 -->
<font color="red">`Butterfly`</font> 支持6种代码高亮样式：

- darker
- pale night
- light
- ocean
- mac
- mac light

修改 <font color="red">`主题配置文件`</font>

```yaml
highlight_theme: light
```

> darker

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071629682.png)

> pale night

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071645203.png)

> light

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071645523.png)

> ocean

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071646214.png)

> mac

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071646352.png)

> mac light

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071647614.png)

<!-- endtab -->

<!-- tab 自定义主题 -->
主题从 3.0 开始，支持使用自定义的代码顔色。

如何自定义主题，请查看下面这篇文章。

[自定义代码配色](https://butterfly.js.org/posts/b37b5fe3/)

<!-- endtab -->
{% endtabs %}

### 代码复制

主题支持代码复制功能

修改 <font color="red">主题配置文件</font>

```yaml
highlight_copy: true
```

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071651983.png)

### 代码框展开/关闭

在默认情况下，代码框自动展开，可设置是否所有代码框都关闭状态，点击<font color="red">`>`</font>可展开代码

- true 全部代码框不展开，需点击<font color="red">`>`</font>打开
- false 代码框展开，有<font color="red">`>`</font>点击按钮
- none 不显示<font color="red">`>`</font>按钮

修改 <font color="red">主题配置文件</font>

```yaml
highlight_shrink: true #代码框不展开，需点击 '>' 打开
```

> 你也可以在post/page页对应的markdown文件front-matter添加highlight_shrink来独立配置。
>
> 当主题配置文件中的 <font color="red">`highlight_shrink` </font>设为true时，可在front-matter添加 <font color="red">`highlight_shrink: false`</font>来单独配置文章展开代码框。
>
> 当主题配置文件中的  <font color="red">`highlight_shrink` </font> 设为false时，可在front-matter添加 <font color="red">`highlight_shrink: true`</font>来单独配置文章收缩代码框。
>

 <font color="red">`highlight_shrink: true`</font>

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071655866.png)

 <font color="red">`highlight_shrink: false`</font>

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071655593.png)

 <font color="red">`highlight_shrink: none`</font>

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071655529.png)

###  代码换行

在默认情况下，Hexo 在编译的时候不会实现代码自动换行。如果你不希望在代码块的区域里有横向滚动条的话，那么你可以考虑开启这个功能。

修改 <font color="red">主题配置文件</font>

```yaml
修改 <font color="red">主题配置文件</font>
```

如果你是使用 highlight 渲染，需要找到你站点的 Hexo 配置文件 <font color="red">`_config.yml`</font>，将 <font color="red">`line_number`</font>改成 <font color="red">`false`</font>:

```yaml
highlight:
  enable: true
  line_number: false # <- 改这里
  auto_detect: false
  tab_replace:
```

如果你是使用 prismjs 渲染，需要找到你站点的 Hexo 配置文件 <font color="red">`_config.yml`</font>，将 <font color="red">`line_number`</font>改成 <font color="red">`false`</font>:

```yaml
prismjs:
  enable: false
  preprocess: true
  line_number: false # <- 改这里
  tab_replace: ''
```

> 设置<font color="red">`code_word_wrap`</font>之前:

![](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071659102.png)

> 设置<font color="red">`code_word_wrap`</font>之后:

![img](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071659236.png)

###  代码高度限制

> 3.7.0 及以上支持

可配置代码高度限制，超出的部分会隐藏，并显示展开按钮。

```yaml
highlight_height_limit: false # unit: px
```

注意：

1. 单位是<font color="red">` px`</font>，直接添加数字，如 200
2. 实际限制高度为<font color="red">` highlight_height_limit + 30 px`</font> ，多增加 30px 限制，目的是避免代码高度只超出highlight_height_limit 一点时，出现展开按钮，展开没内容。
3. 不适用于隐藏后的代码块（ css 设置 display: none）

## 社交图标

Butterfly支持 [font-awesome v6](https://fontawesome.com/icons?from=io)图标.

书写格式 <font color="red">`图标名：url || 描述性文字`</font>

```yaml
social:
  fab fa-github: https://github.com/xxxxx || Github
  fas fa-envelope: mailto:xxxxxx@gmail.com || Email
```

图标名可在这寻找

![img](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071705210.png)

PC:

![img](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071704239.png)

mobile:

![1560603353743](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071705003.png)

## 主页文章节选(自动节选和文章页description)

因为主题UI的关係，主页文章节选只支持自动节选和文章页description。

在butterfly里，有四种可供选择

1. **description**： 只显示description
2. **both**： 优先选择description，如果没有配置description，则显示自动节选的内容
3. **auto_excerpt**：只显示自动节选
4. **false**： 不显示文章内容

修改` 主题配置文件`

```yaml
index_post_content:
  method: 3
  length: 500 # if you set method to 2 or 3, the length need to config
```

`description`在front-matter里添加

![img](https://raw.githubusercontent.com/winstone-su/imageHosting/main/image/202303071706702.png)

## 顶部图

> 如果不要显示顶部图，可直接配置 <font color="red">`disable_top_img: true`</font>

> 顶部图的获取顺序，如果都没有配置，则不显示顶部图。
>
> 1. 页面顶部图的获取顺序：
>
>    各自配置的 top_img > 配置文件的 default_top_img
>
> 2. 文章页顶部图的获取顺序：
>
>    各自配置的 top_img > cover > 配置文件的 default_top_img

配置中的值：

| 配置             | 解释                                                         |
| ---------------- | ------------------------------------------------------------ |
| index_img        | 主页的 top_img                                               |
| default_top_img  | 默认的 top_img，当页面的 top_img 没有配置时，会显示 default_top_img |
| archive_img      | 归档页面的 top_img                                           |
| tag_img          | tag 子页面 的 默认 top_img                                   |
| tag_per_img      | tag 子页面的 top_img，可配置每个 tag 的 top_img              |
| category_img     | category 子页面 的 默认 top_img                              |
| category_per_img | category 子页面的 top_img，可配置每个 category 的 top_img    |

其它页面 （tags/categories/自建页面）和 文章页 的 <font color="red">`top_img`</font> ，请到对应的 md 页面设置<font color="red">`front-matter`</font>中的<font color="red">`top_img`</font>

以上所有的 top_img 可配置以下值

> 3.2.0 以下版本的配置只支持
>
> - 留空，true 和 false - 显示默认的顔色
> - img链接 - 显示所配置的图片
