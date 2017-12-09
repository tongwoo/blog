---
layout: post
title: 'MySQL常用命令'
date: 2016-04-12
author: wutong
tags:  mysql mariadb
---

记录一下经常使用的命令。

```sql
-- 创建只能使用127.0.0.1来进行连接的normal用户,密码是123
CREATE USER 'normal'@'127.0.0.1' IDENTIFIED BY '123';
 
-- 给这个用户所有权限(没有这个用户就创建)
GRANT ALL PRIVILEGES ON *.* TO normal@127.0.0.1 IDENTIFIED BY '123';
```