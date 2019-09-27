---
layout: post
title: '使用ArcGIS开发内网离线WEB地图应用（上）'
date: 2019-09-27
author: wutong
tags:  arcgis map javascript
---

在工作中可能会遇到客户想要一个与外界隔绝仅且供内网使用的web地图应用，本文介绍如何进行内网离线地图开发

## 开发前的思考

 - 地图数据从哪里来？
 - 如果有地图数据之后怎么切分地图为切片？
 - 有了切片时候如何进行加载，什么东西来输出切片？
 - 向地图创建Point、Polygon等覆盖物用什么库？

## 准备工作

 - ArcGIS Server
 - ArcMap
 - ArcGIS API for JavaScript

**ArcGIS Server**

因为用于web，所以最好是切分成同等大小的图片，再进行地图拖动的时候进行动态加载，此软件提供地图服务，比如要素查询，输出地图切片

**ArcMap**

地图数据可以从测绘部门购买也可以网上找一些，一般购买比较贵，在我目前的一个项目中仅一个区价格就要12万元。此软件用于创建编辑地图并发布地图服务到 `ArcGIS Server` ，比如上面所说的切片工作就是 `ArcMap` 来处理

**ArcGIS API for JavaScript**

最重要的开发库，没有它我们无法进行地图应用的前端开发

## 软件安装

### ArcGIS Server

自行百度破解版安装即可，安装完成后需要将 `https` 改成 `http`

**修改方式**

找到 `ArcGIS Server Manager` 图标打开后出现 `https://localhost:6080/arcgis/manager/`

将地址栏中的 `manager` 换成 `admin` 出现下图画面

![ArcGIS Server Manager](/screenshot/2019-09-27/arcgis-server-admin.png)

输入之前配置的用户名和密码登录后，进行如下操作：

 - 在页面下找到 `Resources` 段，并点击 `security` 链接
 - 在 `security` 页面下找到 `Resources` 段，并点击 `config` 链接
 - 在 `config` 页面下找到 `Supported Operations` 段，并点击 `update` 链接
 - 在 `update` 页面下找到 `Security Configuration` 选区，并点击 `Protocol` 右边的下拉框，将其改为 `Http Only`，然后点击 `Update` 按钮完成修改（需要等一会时间生效）
 
 
### ArcGIS Map

自行百度破解版安装即可

### ArcGIS API for JavaScript

访问 [https://developers.arcgis.com/downloads/apis-and-sdks?product=javascript](https://developers.arcgis.com/downloads/apis-and-sdks?product=javascript) 页面下载所需要的JS库备用

## 地图切片

打开 `ArcGIS Map` 应用之后打开地图数据，我这里用到的数据是 `gdb` 格式，执行如下相关操作进行切片并发布为服务

![概览](/screenshot/2019-09-27/arcgis-map.png)

1、打开菜单栏中的 `File` - `Share As` - `Service...`

![第一步](/screenshot/2019-09-27/arcgis-step-1.png)

2、如果没有 `Server`，直接新建一个，然后按照如下图示继续

![第二步](/screenshot/2019-09-27/arcgis-step-2.png)

![第三步](/screenshot/2019-09-27/arcgis-step-3.png)

![第四步](/screenshot/2019-09-27/arcgis-step-4.png)

![第五步](/screenshot/2019-09-27/arcgis-step-5.png)

3、以上步骤完成之后，静待切片完成，可以在 `Catalog` 窗口中右击创建的服务选择 `View Cache Status...` 查看当前进度

![第六步](/screenshot/2019-09-27/arcgis-step-6.png)

4、打开 `ArcGIS Server Manager` 进入首页查看发布服务情况

![第七步](/screenshot/2019-09-27/arcgis-step-7.png)

5、点击服务标题后再进入`功能` 页面查看服务接口地址并记录下来，后面将用于地图加载

![第八步](/screenshot/2019-09-27/arcgis-step-8.png)
