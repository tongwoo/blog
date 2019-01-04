---
layout: post
title: '使用Docker来配置商派产品运行环境'
date: 2019-01-04
author: wutong
tags:  linux php nginx docker
---

人员流失太多，不得已也要维护2个商城，其中一个是商派的ECStore，自己的机器用的PHP7.1，跑不起来，Zend Guard Loader 5.6 之后Zend不再进行维护，遂自己建个运行商派产品的容器


## 安装Docker

打开 [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop) 选择自己需要的版本安装

## 安装系统

```bash
docker pull centos:7
```

## 安装运行环境

交互式运行CentOS容器

```bash
docker run -i -t centos:7
```


### 安装Nginx

在当前命令行中进行配置Nginx源，建立 `/etc/yum.repos.d/nginx.repo` 并粘贴如下内容

```bash
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/7/$basearch/
gpgcheck=0
enabled=1
```

建立后开始安装

```bash
yum install nginx
```

修改 `/etc/nginx/nginx.conf` 第一行加入 `daemon off`

因版本不同 `/etc/nginx/` 下的配置文件不太相同，如果没有 `fastcgi.conf` 文件自己建立一个并粘贴如下内容

```bash
fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
fastcgi_param  QUERY_STRING       $query_string;
fastcgi_param  REQUEST_METHOD     $request_method;
fastcgi_param  CONTENT_TYPE       $content_type;
fastcgi_param  CONTENT_LENGTH     $content_length;

fastcgi_param  SCRIPT_NAME        $fastcgi_script_name;
fastcgi_param  REQUEST_URI        $request_uri;
fastcgi_param  DOCUMENT_URI       $document_uri;
fastcgi_param  DOCUMENT_ROOT      $document_root;
fastcgi_param  SERVER_PROTOCOL    $server_protocol;
fastcgi_param  REQUEST_SCHEME     $scheme;
fastcgi_param  HTTPS              $https if_not_empty;

fastcgi_param  GATEWAY_INTERFACE  CGI/1.1;
fastcgi_param  SERVER_SOFTWARE    nginx/$nginx_version;

fastcgi_param  REMOTE_ADDR        $remote_addr;
fastcgi_param  REMOTE_PORT        $remote_port;
fastcgi_param  SERVER_ADDR        $server_addr;
fastcgi_param  SERVER_PORT        $server_port;
fastcgi_param  SERVER_NAME        $server_name;

# PHP only, required if PHP was built with --enable-force-cgi-redirect
fastcgi_param  REDIRECT_STATUS    200;
```


### 安装PHP5.6

配置 php 的源

```bash
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

安装 php

```bash
yum install -y php56w php56w-bcmath php56w-cli php56w-common php56w-dba php56w-devel php56w-embedded php56w-enchant php56w-fpm php56w-gd php56w-imap php56w-interbase php56w-intl php56w-ldap php56w-mbstring php56w-mcrypt php56w-mssql php56w-mysqlnd php56w-odbc php56w-opcache php56w-pdo php56w-pear php56w-pecl-apcu php56w-pecl-apcu-devel php56w-pecl-gearman php56w-pecl-geoip php56w-pecl-igbinary php56w-pecl-igbinary-devel php56w-pecl-imagick php56w-pecl-imagick-devel php56w-pecl-memcache php56w-pecl-memcached php56w-pecl-mongodb php56w-pecl-redis php56w-pecl-xdebug php56w-pgsql php56w-phpdbg php56w-process php56w-pspell php56w-recode php56w-snmp php56w-soap php56w-tidy php56w-xml php56w-xmlrpc 
```

安装 zend-loader 扩展（注意32位还是64位）

```bash
#下载扩展包
wget http://downloads.zend.com/guard/7.0.0/zend-loader-php5.6-linux-x86_64_update1.tar.gz
#解压
tar -xzvf zend-loader-php5.6-linux-x86_64_update1.tar.gz
#将扩展拷贝到php扩展目录，提示存在请覆盖
cp *.so /usr/lib64/php/modules/
```

查看php是否能正常运行

```bash
php -v

PHP 5.6.38 (cli) (built: Sep 15 2018 08:16:33)
Copyright (c) 1997-2016 The PHP Group
Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    with Zend Guard Loader v3.3, Copyright (c) 1998-2015, by Zend Technologies
    with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies
    with Xdebug v2.5.5, Copyright (c) 2002-2017, by Derick Rethans
```

可以看到扩展也都装上去了

### 杂项配置

将 `php-fpm` 运行的用户和组变更为 `nginx`
将 `/var/lib/php` 的用户和组变更为 `nginx`

### 配置ZendLoader

打开 `php.ini` 粘贴如下内容，如果想要有更好的扩展性最好是挂载宿主机的配置文件

```bash
#商派要求下面的参数为-1
always_populate_raw_post_data = -1
#ZendLoader配置
zend_loader.enable=1
zend_loader.disable_licensing=0
zend_loader.obfuscation_level_support=3
zend_loader.license_path=商派许可证文件路径
```

## 创建镜像

在交互式环境下做完上面的事情后，输入 `exit` 退出

查看运行过的容器

```bash
docker ps -a

CONTAINER ID   IMAGE        COMMAND       CREATED      STATUS                     PORTS      NAMES
b1d45882623f   centos:7     "/bin/bash"   5 hours ago  Exited (0) 5 hours ago                admiring_newton
```

对刚才使用的centos容器进行扩展并建立镜像，也可以使用 `Dockerfile`

```bash
docker commit -m "CentOS7-Nginx-PHP56-ZendGuardLoader" b1d45882623f tongwoo/centos7-nginx-php56-zend-guard-loader
```

创建成功后，为了以后更方便在其他机器使用，可以考虑放到 docker hub 仓库中

```bash
docker login
docker push tongwoo/centos7-nginx-php56-zend-guard-loader
```

## 运行镜像

因为容器只能有一个主进程，但是要运行代码需要启动 `php-fpm` 和 `nginx`，所以可以考虑建立一个脚本 `/app/runapp` 并增加执行权限

```bash
!#/usr/bin/sh
php-fpm
nginx
```

为了能顺利运行宿主机的代码，在运行容器的时候需要挂载宿主机的 `源代码目录、php自定义配置文件、Nginx配置文件` ，其中 `php自定义配置文件` 我们可能想覆盖 `php.ini` 的配置，比如商派的许可证文件路径，`Nginx配置文件` 自定义主机配置等

执行下面的命令来运行容器

```bash
docker run -p 3000:80 -v /web/TianDiShop:/var/www/html/TianDiShop -v /web/TianDiShop/tiandi.conf:/var/www/html/tiandi.conf -v /web/TianDiShop/tiandi.ini:/etc/php.d/tiandi.ini tongwoo/centos7-nginx-php56-zend-guard-loader /app/runapp
```

这个命令做了如下操作：

 - 将宿主机的3000端口转发到容器的80端口
 - 将宿主机的/web/TianDiShop目录映射到容器的/var/www/html/TianDiShop
 - 将宿主机的/web/TianDiShop/tiandi.conf配置文件映射到容器的/var/www/html/tiandi.conf
 - 将宿主机的/web/TianDiShop/tiandi.ini配置文件映射到容器的/etc/php.d/tiandi.ini

如果想要守护允许则加上 `-d` 选项

访问 `http://127.0.0.1:3000` 可以看到宿主机的商城显示出来了
    

