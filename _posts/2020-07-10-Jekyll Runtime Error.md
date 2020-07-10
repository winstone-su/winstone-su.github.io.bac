---

layout: post

title: Jekyll 运行错误

categories: Jekyll

description: 

keywords: Jekyll

topmost: false

---

 <font color= "red">Jekyll</font>  运行时发生错误:

```shell
/Library/Ruby/Gems/2.6.0/gems/bundler-2.1.4/lib/bundler/runtime.rb:312:in `check_for_activated_spec!':
You have already activated i18n 1.8.3, but your Gemfile requires i18n 0.9.5.
Prepending `bundle exec` to your command may solve this. (Gem::LoadError)
```

​	解决办法:

```shell
bundle update
```

 修改 `Gemfile.lock` 将 `i18n` 配置升级为`1.8.3`

```shell
bundle exec jekyll serve
```

再次运行项目
