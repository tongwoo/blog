---
layout: post
title: '基于一条线做垂直平行于此线的新线'
date: 2019-09-10
author: wutong
tags:  javascript
---

最近遇到一个功能，给一条线，给一个离线的距离，再做一条线，新的线要垂直平行于之前的线，且距离为给的距离，复习了几何知识，最终解决了这一问题

## 效果示例

<iframe src="http://codedemo.org/point-parallel" style="width:100%;height:600px;border:0;"></iframe>


## 计算方式

假如有如下 AB 线段，做 CD 线段

![图1](/screenshot/2019-09-10/point-1.png)

先根据AB点做一个直角三角形

![图2](/screenshot/2019-09-10/point-4.png)

根据 A点 和 B点 的位置，可以得知 AF、BF 的距离，根据三角公式得知 AB距离和角b的角度

![图3](/screenshot/2019-09-10/point-3.png)

根据给定的距离，再做一个垂直于A点的直角三角形，因为是垂直关系，可以得知 ∠a = 90°- ∠b

因为AC距离是已知的，所以根据三角公式得知 sin∠a = EC / AC，则偏移后的y点为 A.y+EC

再根据三角公式得知 AE<sup>2</sup> = AC<sup>2</sup> - EC<sup>2</sup> 算出 AE 距离，则偏移后的x点为 A.x+AE

因为同等大小的关系，所以可以直接得出 D点坐标
