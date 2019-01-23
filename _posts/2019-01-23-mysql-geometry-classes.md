---
layout: post
title: 'MySQL的几何类'
date: 2019-01-23
author: wutong
tags:  mysql mariadb
---

整理了MySQL的几何类对应的图示和说明

## geometry 数据类型的类层次结构图

黄色为抽象类，蓝色为可实例化，如图：

![](/screenshot/2019-01-23/geometry-layer.gif)

## Point

Point 是表示单个位置的零维对象，就是一个 `点`，比如地图中的经纬度

## MultiPoint

同 Point，不过是一个 Point 集合

## LineString

LineString 是一个一维对象，表示一系列点和连接这些点的线段，如图：

![](/screenshot/2019-01-23/linestring.gif)

**如图中所示：**

 - 图 1 显示的是一个简单、非闭合的 LineString 实例。
 - 图 2 显示的是一个不简单、非闭合的 LineString 实例。
 - 图 3 显示的是一个闭合、简单的 LineString 实例，因此是一个环。
 - 图 4 显示的是一个闭合、不简单的 LineString 实例，因此不是一个环。
 
## MultiLineString
 
MultiLineString 是零个或更多 LineString 实例的集合，如图：
 
![](/screenshot/2019-01-23/multilinestring.gif)
 
**如图中所示：**
 
 - 图 1 显示的是一个简单的 MultiLineString 实例，其边界是其两个 LineString 元素的四个端点。
 - 图 2 显示的是一个简单的 MultiLineString 实例，因为只有 LineString 元素的端点相交。边界是两个不重叠的端点。
 - 图 3 显示的是一个不简单的 MultiLineString 实例，因为它的其中一个 LineString 元素的内部出现了相交。此 MultiLineString 实例的边界是四个端点。
 - 图 4 显示的是一个不简单、非闭合的 MultiLineString 实例。
 - 图 5 显示的是一个简单、非闭合的 MultiLineString。它没有闭合是因为它的 LineStrings 元素没有闭合。而其简单的原因在于，其任何 LineStrings 实例的内部都没有出现相交。
 - 图 6 显示的是一个简单、闭合的 MultiLineString 实例。它为闭合的是因为它的所有元素都是闭合的。而其简单的原因在于，其所有元素都没有出现内部相交现象。
 
## Polygon
 
Polygon 是存储为一系列点的二维表面，这些点定义一个外部边界环和零个或多个内环，可以从至少具有三个不同点的环中构建一个 Polygon 实例，Polygon 实例也可以为空，Polygon 的外部环和任意内部环定义了其边界，环内部的空间定义了 Polygon 的内部，如图：
 
![](/screenshot/2019-01-23/polygon.gif)
 
**如图中所示：**
 
 - 图 1 是由外部环定义其边界的 Polygon 实例。
 - 图 2 是由外部环和两个内部环定义其边界的 Polygon 实例。内部环内的面积是 Polygon 实例的外部环的一部分。
 - 图 3 是一个有效的 Polygon 实例，因为其内部环在单个切点处相交。
 
## MultiPolygon
 
MultiPolygon 实例是零个或更多个 Polygon 实例的集合，如图：
 
![](/screenshot/2019-01-23/multipolygon.gif)
 
**如图中所示：**
 
 - 图 1 是一个包含两个 Polygon 元素的 MultiPolygon 实例。边界由两个外环和三个内环界定。
 - 图 2 是一个包含两个 Polygon 元素的 MultiPolygon 实例。边界由两个外环和三个内环界定。这两个 Polygon 元素在切点处相交。
 
