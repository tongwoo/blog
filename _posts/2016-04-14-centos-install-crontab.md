---
layout: post
title: 'CentOS最小安装没有crontab命令'
date: 2016-04-14
author: wutong
tags:  linux centos
---

CentOS最小安装默认不包含“crontab”服务，解决它。

## CentOS 6

#### 安装依赖包

```bash
yum install vixie-cron
```

#### 自启动这个包

```bash
/sbin/chkconfig crond on
/etc/init.d/crond start
```

## CentOS 7

```bash
yum install cronie
```