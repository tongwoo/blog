---
layout: post
title: '基于位置服务 - 按照远近进行排序(MySQL)'
date: 2018-07-08
author: wutong
tags:  lbs php mysql
---

在开发中可能会遇到根据经纬度来检索附近的XX情况，范围检索可以直接算出上下左右的边界并进行检索，如果要按照远近程度进行排序，则需要进行换算。

## 解决方式

创建自定义函数，排序的时候根据自定义函数算出的距离来进行升降排序

## 创建函数

执行如下SQL来创建一个获取距离的自定义函数。

```sql
DROP FUNCTION IF EXISTS point_distance;
DELIMITER //
CREATE FUNCTION `point_distance`(
    `lng1` float(9,6) ,
    `lat1` float(9,6),
    `lng2` float(9,6) ,
    `lat2` float(9,6)
) RETURNS MEDIUMINT
    COMMENT '计算两个坐标点之间的距离'
BEGIN
    declare distance MEDIUMINT;
    declare radius MEDIUMINT;
    -- 地球半径
    set radius = 6370856;
    -- 距离（米）
    set distance = (2*ATAN2(SQRT(SIN((lat1-lat2)*PI()/180/2)
        *SIN((lat1-lat2)*PI()/180/2)+
        COS(lat2*PI()/180)*COS(lat1*PI()/180)
        *SIN((lng1-lng2)*PI()/180/2)
        *SIN((lng1-lng2)*PI()/180/2)),
        SQRT(1-SIN((lat1-lat2)*PI()/180/2)
        *SIN((lat1-lat2)*PI()/180/2)
        +COS(lat2*PI()/180)*COS(lat1*PI()/180)
        *SIN((lng1-lng2)*PI()/180/2)
        *SIN((lng1-lng2)*PI()/180/2))))*radius;
    return distance;
END//
DELIMITER ;
```

## 业务实现

查找门店并按照离我的位置由近到远排列

```sql
SELECT 
    `name`,point_distance(当前经度，当前纬度，表里的经度，表里的纬度) AS distance
FROM shop ORDER BY  distance ASC;
```

结果：

```sql
+----+------------+-----------+-----------------+----------+
| id | longitude  | latitude  | name            | distance |
+----+------------+-----------+-----------------+----------+
|  1 | 120.275731 | 31.548376 | 体育中心店      |      795 |
|  2 | 120.292145 | 31.567969 | 开源大桥        |     2315 |
|  3 | 120.373998 | 31.507401 | 创新园          |     9656 |
+----+------------+-----------+-----------------+----------+
```