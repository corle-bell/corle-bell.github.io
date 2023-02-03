---
layout:     post
title: UIParitcles
subtitle:   副标题
date:       2021-07-29
author:     坏人
header-img: img/the-first.png
catalog: false
tags:
    - Unity杂谈
---


在使用了 OnRenderImage 函数的时候, UIParticles在ui上所绘制的图像会看不到。
需要给OnRenderImage添加特性 ImageEffectOpaque  让OnRenderImage在执行完不透明的pass以后就开始处理。不过具体要看是否影响到效果。如果影响效果则不可取。

[参考文章:](https://www.codeleading.com/article/75423758975/)