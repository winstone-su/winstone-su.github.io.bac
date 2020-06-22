---
layout: post
title: iOS中使用 `MJExtension`处理OC里的`id`关键字
categories: iOS
description: 
keywords: iOS
topmost: true
---

​利用`MJExtension` 解析json -> model 遇到OC关键字`id`,处理方法:

在 Model 中使用方法:

```objective-c
+(NSDictionary *)mj_replacedKeyFromPropertyName
{
    return @{@"ID":@"id"};
}
```



或者写个统一的类处理相同的请求:

```objective-c
 [Xxx mj_setupReplacedKeyFromPropertyName:^NSDictionary *{
        return @{
                   @"ID" : @"id",
               };
    }];
```

