---
layout: post
title: 'Mac下配置Apache的fastcgi扩展与PHP'
date: 2018-08-22
author: wutong
tags:  linux php apache
---

同事用的都是apache，我个人用的nginx，某些重写需要搞两种版本，之前用的module方式今天想尝试下fastcgi模式，记录下过程。


### 下载fastcgi扩展源码

进入 [http://httpd.apache.org/download.cgi](http://httpd.apache.org/download.cgi) 页面找到 「Apache mod_fcgid FastCGI module for Apache HTTP Server」的标题，下载一个源码包。

### 编译fastcgi扩展

解压后进入源码目录执行如下命令：

```bash
./configure.apxs
make
make install
```
如果系统有多个版本的apache httpd的话，保证当前用的是httpd命令是你想要的版本，否则编译后 `mod_fcgid.so` 放置的目录不正确。

### 配置fastcgi

我直接新建一个 `VirtualHost` 来创建新的一个主机，配置如下：

```apache
<VirtualHost *:8080>
    DocumentRoot /web/project
    ServerName project.local
    <Directory "/web/project">
        AddHandler fcgid-script .php
        #FcgidWrapper 参数值为你的php-cgi路径
        FcgidWrapper /usr/local/Cellar/php@7.1/7.1.20/bin/php-cgi .php
    		Options +ExecCGI
        Require all granted
    </Directory>
</VirtualHost>
```

### 重启apache httpd 服务

```bash
brew services restart httpd
```