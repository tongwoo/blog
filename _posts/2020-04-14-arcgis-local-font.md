---
layout: post
title: 'ArcGIS使用本地字体'
date: 2020-04-14
author: wutong
tags:  arcgis javascript
---

如果在离线环境下使用`TextSymbol`会出现找不到字体的问题，本文记录一下如何解决这个问题

# 原因

默认加载的是网页字体，所以会出现地图上的文字显示不了且控制台报错

# 解决办法

## 第一步

使用本地字体，且格式得是 pbf 格式，在网上找个转换好的字体下载下来,并部署到一个能web访问的地址，比如：http://test.com/msyh/msyh-regular  

链接: https://pan.baidu.com/s/15gD7DJ7Ajctb4fJQoEccWQ 提取码: ieq7

## 第二步

在入口处修改加载字体文件的配置

```
require(["esri/config"], function(esriConfig) {
    esriConfig.fontsUrl = "https://myserver.com/fonts";
});
```

## 第三步

设置字体

```
let textSymbol = {
    type: "text",
    font: {
        family:'msyh',
        size: 12,
    }
};
```