---
layout: post
title: 'MySQL设置默认编码'
date: 2016-11-09
author: wutong
tags:  linux mysql mariadb
---

修改 /etc/my.cnf 文件

```code
[client]
default-character-set=utf8

[mysqld]
character-set-server=utf8
```