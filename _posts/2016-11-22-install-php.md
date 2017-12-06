---
layout: post
title: '安装PHP运行环境'
date: 2016-11-22
author: wutong
tags:  linux php mysql mariadb apahce
---

经常要手动配置客户的web服务器，比较耗费时间，索性做个记录以便下次直接复制粘贴。


## 增加仓库

### CentOS/RHEL 7.x:

```bash
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

### CentOS/RHEL 6.x:

```bash
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
```

## 安装PHP及其扩展包

### 按需安装

```bash
yum install php71w-bcmath php71w-cli php71w-common php71w-dba php71w-devel php71w-embedded php71w-enchant php71w-fpm php71w-gd php71w-imap php71w-interbase php71w-intl php71w-ldap php71w-mbstring php71w-mcrypt php71w-mysqlnd php71w-odbc php71w-opcache php71w-pdo php71w-pdo_dblib php71w-pear php71w-pecl-apcu php71w-pecl-apcu-devel php71w-pecl-geoip php71w-pecl-igbinary php71w-pecl-igbinary-devel php71w-pecl-imagick php71w-pecl-imagick-devel php71w-pecl-memcached php71w-pecl-mongodb php71w-pecl-redis  php71w-pgsql php71w-process php71w-pspell php71w-recode php71w-snmp php71w-soap php71w-tidy php71w-xml php71w-xmlrpc
```

### 全部安装

```bash
yum install -y php71w-bcmath php71w-cli php71w-common php71w-dba php71w-devel php71w-embedded php71w-enchant php71w-fpm php71w-gd php71w-imap php71w-interbase php71w-intl php71w-ldap php71w-mbstring php71w-mcrypt php71w-mysql php71w-mysqlnd php71w-odbc php71w-opcache php71w-pdo php71w-pdo_dblib php71w-pear php71w-pecl-apcu php71w-pecl-apcu-devel php71w-pecl-geoip php71w-pecl-igbinary php71w-pecl-igbinary-devel php71w-pecl-imagick php71w-pecl-imagick-devel php71w-pecl-memcached php71w-pecl-mongodb php71w-pecl-redis php71w-pecl-xdebug php71w-pgsql php71w-phpdbg php71w-process php71w-pspell php71w-recode php71w-snmp php71w-soap php71w-tidy php71w-xml php71w-xmlrpc
```

## 安装MySQL

```bash
yum install -y mariadb mariadb-server
```
打开 /etc/my.cnf 修改一下默认编码

```bash
[client]
default-character-set=utf8
[mysqld]
character-set-server=utf8
```

启动数据库服务

```bash
systemctl start mariadb
```
初始化数据库，根据提示完成

```bash
mysql_secure_installation
```
初始化过程

```bash
[root@iZhp38fu0lgb2Z ~]# mysql_secure_installation

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] Y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

## Web服务器

### 安装Apache和PHP模块

```bash
yum install -y httpd
yum install -y mod_php71w
```

修改默认的配置文件：/etc/httpd/conf/httpd.conf

```apacheconf
#不修改会有提示
ServerName 127.0.0.1:80
#根据需要配置相关参数
DocumentRoot "/web"
<Directory "/web">    
    AllowOverride All
</Directory>
```

进入 /etc/httpd/conf.d 目录新建一个配置文件，比如：wutong.conf

增加一个Virtual配置段来当做虚拟主机

```apacheconf
<VirtualHost *:80>
    #域名
    ServerName wutong.me
    #其他域名
    ServerAlias blog.wutong.me
    #网站目录
    DocumentRoot "/web"
    #错误日志
    ErrorLog /tmp/error.log
</VirtualHost>
```

启动Apache

```bash
service httpd start
```


### 安装Nginx 

```bash
yum install -y nginx
```

### 配置Nginx

进入 /etc/nginx/conf.d 目录新建一个配置文件，比如：wutong.conf

增加一个server配置段来当做虚拟主机

```nginx
server {
    #网站目录全路径
    root /web/explorer;
    #默认页
    index index.html index.php;
    #监听端口
    listen 80;
    #域名,多个域名用空格隔开
    server_name 140.143.45.28 www.shai.com shai.com;
    #错误日志路径
    error_log /web/explorer/logs/error_log error;
    #是否启用目录浏览
    autoindex on;

    #如果用Yii、Laravel等之类的框架则用下面这段配置
    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    #如果你用的是ThinkPHP框架则用下面这段配置
    location / {
        if (!-e $request_filename) {
            rewrite  ^(.*)$  /index.php?s=$1  last;
            break;
        }
    }
    #处理PHP格式的文件
    location ~ \.php$ {
        #try_files $uri=404;
        include /etc/nginx/fastcgi.conf;
        fastcgi_pass 127.0.0.1:9000;
    }
}
```

启动 Nginx

```bash
service nginx start
```

启动 PHP-FPM

```bash
service php-fpm start
```

