---
layout: post
title: 'MySQL常用列类型存储要求'
date: 2016-03-28
author: wutong
tags:  linux mysql
---

根据类别列出了MySQL支持的每个列类型的存储需求。


### 数值类型存储需求

| **列类型** | **存储需求** |
|---|---|
| TINYINT | 1个字节 |
| SMALLINT | 2个字节 |
| MEDIUMINT | 3个字节 |
| INT, INTEGER | 4个字节 |
| BIGINT | 8个字节 |
| FLOAT(*p*) | 如果0 <= *p* <= 24为4个字节, 如果25 <= *p* <= 53为8个字节 |
| FLOAT | 4个字节 |
| DOUBLE [PRECISION], item REAL | 8个字节 |
| DECIMAL(*M*,*D*), NUMERIC(*M*,*D*) | 变长；参见下面的讨论 |
| BIT(*M*) | 大约(*M*+7)/8个字节 |


### 日期和时间类型的存储需求

| **列类型** | **存储需求** |
|---|---|
| DATE | 3个字节 |
| DATETIME | 8个字节 |
| TIMESTAMP | 4个字节 |
| TIME | 3个字节 |
| YEAR | 1个字节 |

### 字符串类型的存储需求

| **列类型** | **存储需求** |
|---|---|
| CHAR(*M*) | *M*个字节，0 <= *M* <= 255 |
| VARCHAR(*M*) | *L*+1个字节，其中*L* <= *M* 且0 <= *M* <= 65535(参见下面的注释) |
| BINARY(*M*) | *M*个字节，0 <= *M* <= 255 |
| VARBINARY(*M*) | *L*+1个字节，其中*L* <= *M* 且0 <= *M* <= 255 |
| TINYBLOB, TINYTEXT | *L*+1个字节，其中*L* < 2<sup>8</sup> |
| BLOB, TEXT | *L*+2个字节，其中*L* < 2<sup>16</sup> |
| MEDIUMBLOB, MEDIUMTEXT | *L*+3个字节，其中*L* < 2<sup>24</sup> |
| LONGBLOB, LONGTEXT | *L*+4个字节，其中*L* < 2<sup>32</sup> |
| ENUM('*value1*','*value2*',...) | 1或2个字节，取决于枚举值的个数(最多65,535个值) |
| SET('*value1*','*value2*',...) | 1、2、3、4或者8个字节，取决于set成员的数目(最多64个成员) |
