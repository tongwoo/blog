---
layout: post
title: '安装TelnetServer'
date: 2018-05-09
author: wutong
tags:  linux telnet
---

升级OpenSSH最好先装下TelnetServer

## CentOS 6 安装方式

#### 安装包
```bash
yum install telnet-server
```

#### 启动服务

```bash
chkconfig telnet on
service xinetd start
```



## CentOS 7 安装方式

#### 安装包
```bash
yum install telnet-server
yum install xinetd
```

#### 启动服务

```bash
systemctl enable telnet.socket
systemctl start telnet.socket
systemctl start xinetd
```

## 测试连接

```bash
wutong@tongwoo:~$ telnet 10.211.55.6
Trying 10.211.55.6...
Connected to centos-linux-65.shared.
Escape character is '^]'.
Password:
```
连接不上注意防火墙有没有禁掉23端口