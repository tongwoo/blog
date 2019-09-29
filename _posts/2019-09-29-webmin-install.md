---
layout: post
title: 'Webmin安装'
date: 2019-09-29
author: wutong
tags:  webmin linux centos
---

Webmin是一个网页端的图形化的Linux管理，在CentOS上安装它

## 安装

在命令行下输入如下代码并按回车

```bash
(echo "[Webmin]
name=Webmin Distribution Neutral
baseurl=http://download.webmin.com/download/yum
enabled=1
gpgcheck=1
gpgkey=http://www.webmin.com/jcameron-key.asc" >/etc/yum.repos.d/webmin.repo;
yum -y install webmin)
```

添加端口

```bash
firewall-cmd --zone=public --add-port=10000/tcp --permanent
```

重载防火墙

```bash
firewall-cmd --reload
```

## 使用

在浏览器中输入 `https://你的IP:10000` 默认端口是10000，在登录页面中输入你的Linux用户名和密码登录即可

![Webmin](/screenshot/2019-09-29/webmin-ui.png)