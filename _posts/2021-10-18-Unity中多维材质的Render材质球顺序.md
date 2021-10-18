---
layout:     post
title:      Unity中多维材质的Render材质球顺序
subtitle:   Unity中多维材质的Render材质球顺序
date:       2021-10-18
author:     坏人
header-img: img/the-first.png
catalog: false
tags:
    - Unity杂谈
---

Renderer存在多个材质的情况下，是按照绘制模型的顶点索引顺序决定的。
假如第一个三角面绘制使用了材质A，第二个面使用了材质B。那么在导入unity后的材质数组就是[材质A, 材质B]