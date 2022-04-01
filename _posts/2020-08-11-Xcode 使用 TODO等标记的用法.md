---
layout: post
title: Xcode 使用 TODO、FIXME、!!!、???、MARK标记用法
categories: Xcode
description: 
keywords: Xcode,iOS
topmost: false
---

## 基础知识：

* `MARK`: 标记，和#pragma mark效果类似，使用方法 `// MARK:`
* TODO`: 标示处有功能代码待编写，使用方法  `// TODO:
* `FIXME`: 标示处代码需要修正，使用方法： `//FIXME`:
* `!!!`: 标示处代码需要注意，使用方法: `//!!!` 
* ???`: 标示处代码有疑问，使用方法： `//???`

## 基本用法:

* 单独使用:

```objective-c
//MARK: 追攀更觉相逢晚，谈笑难忘欲别前
```

* 组合使用： 添加 `-` ，两个 `-` 之间的就会被算做一组

```objective-c
// MARK: - 井底点灯深烛伊,共郎长行莫围棋
// TODO:   玲珑骰子安红豆,入骨相思知不知
// TODO:   愿我如星君如月,夜夜流光相皎洁
// MARK: - 妾弄青梅凭短墙,君骑白马傍垂杨
// FIXME:  愿得红罗千万匹,漫天匝地绣鸳鸯
// MARK: - 独来独往银粟地,一行一步玉沙声
// !!!:    无人与我立黄昏,无人问我粥可温
// ???:    寒夜读书忘却眠，锦衾香尽炉无烟
```

![img]({{ site.url }}/assets/images/202008/0811-1.png)

![img]({{ site.url }}/assets/images/202008/0811-2.png)



## 子标注

```objective-c
//MARK: 追攀更觉相逢晚，谈笑难忘欲别前
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender {
    //TODO: 夜深忽梦少年事，梦啼妆泪红阑干
    if (flag) {
        
    }else{
        
    }
    //TODO:  春风得意马蹄疾,一日看尽长安花
}
```



![img]({{site.url }}/assets/images/202008/0811-3.png)

