---
layout: post
title: ConstraintLayout-constraintDimensionRatio属性
categories: Android
description: 
keywords: Android
topmost: false
---



### h和w参数的解释

> 这里我们还需要解释一下app:layout_constraintDimensionRatio的值里面的h和w是什么意思。一般来说，加上h的意思就是，h之后的比例是以w为基础去设置h，即h = w * ratio。反之，写上w的意思是，w = h / ratio （因为 ratio = w / h 代表宽高比）。