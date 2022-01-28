---
layout:     post
title:      Unity Dynamic batch 动态合批的规则及注意事项
subtitle:   Unity Dynamic batch 动态合批的规则及注意事项
date:       2022-01-26
author:     坏人
header-img: img/the-first.png
catalog: false
tags:
    - Unity杂谈
---


检查Dynamic Batching的规则，可以简单概括为以下几条：

1.  一般情况下，Unity仅支持对Meshes小于900顶点的物体进行Dynamic Batching，如果Shader里使用了顶点位置，法线，UV值，则仅支持300顶点以下的物体；如果使用顶点位置，法线，UV0，UV1和Tangent向量，则仅支持180顶点以下的物体。
2.  如果两个物体的scale刚好是呈镜像的，如scale分别为(-1,-1,-1)或(1,1,1)，他们不会被Dynamic Batching。
3.  引用材质实例不同的物体不会被Dynamic Batching，即使两个物体的材质本质上没有任何不同。这句话的理解有点绕，简单举例就是说，相同的材质实例化了两份，分别被A和B引用了，那么A和B是不会被Dynamic Batching的，因为他们引用的是两个不同的实例。
4.  拥用lightmaps的物体将不会被Dynamic Batching，除非他们指向了lightmap的同一部分。
5.  拥有多Pass通道的Shader的物体不会被Dynamic batching。
6.  合批之后的单个mesh的顶点数不能超过64K

![](https://img-blog.csdnimg.cn/20181107210913764.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpemkzMjk=,size_16,color_FFFFFF,t_70)

转载自

https://blog.csdn.net/qizi329/article/details/83831871?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1.pc_relevant_paycolumn_v3&utm_relevant_index=2