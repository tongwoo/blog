---
layout: post
title: 'CSS margin-top 不生效'
date: 2015-03-11
author: wutong
tags:  css
---

### 原因

盒子没有获得 haslayout 造成 margin-top无效

### 解决办法

 - 在父层div加上 overflow:hidden；
 - 把margin-top外边距改成padding-top内边距 ；
 - 父元素产生边距重叠的边有不为 0 的 padding 或宽度不为 0 且 style 不为 none 的 border。 父层div加： padding-top: 1px;
 - 让父元素生成一个 block formating context

### 以下属性可以实现 block formating context

```code
float: left/right
position: absolute
isplay: inline-block/table-cell(或其他 table 类型)
overflow: hidden/auto
```
