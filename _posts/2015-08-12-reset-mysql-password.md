---
layout: post
title: '恢复MySQL密码'
date: 2015-08-12
author: wutong
tags:  linux mysql mariadb
---

MySQL密码忘记了怎么办？

### 停止mysql服务
```bash
service stop mysqld
```

### 不带权限启动mysql
```bash
mysqld --skip-grant-tables
```

### 另开命令行输入
```bash
mysql -uroot
use mysql;
UPDATE `user` SET password=PASSWORD('你的密码') WHERE user='你的用户名';
```

### 关闭之前的命令行重新启动mysql服务
```bash
service start mysqld
```