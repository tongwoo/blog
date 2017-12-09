---
layout: post
title: 'CentOS安装svn server'
date: 2015-12-03
author: wutong
tags:  centos svn
---

搭建一台SVN服务器。

### 安装

安装 svn server 使用 httpd 的 mod_dav_svn 模块，所以第一步就是安装 httpd

```bash
yum install httpd
```

然后安装 mod_dav_svn

```bash
yum install mod_dav_svn
```

安装完成后会在 /etc/httpd/conf.d 目录生成一个 subversion.conf 配置文件，更改里面的配置

```bash
#用于连接的端口号
listen 2048
#用于连接的域名
ServerName subversion.wutong.me
#用浏览器浏览的时候不显示目录结构
Options -Indexes
DAV svn
#SVN仓库目录
SVNParentPath /mnt/svn_repository
AuthType Basic
#连接svn的欢迎信息
AuthName "Welcome to Sherlock Wooton's SVN server."
#svn用户列表
AuthUserFile /mnt/svn_repository/svn_user
#svn用户授权列表
AuthzSVNAccessFile /mnt/svn_repository/svn_user_auth
Require valid-user
```

因为我要使用域名，所以使用了这样的配置

```bash
#代表svn的仓库目录，以后就在这个路径下建立仓库
SVNParentPath

#代表了svn用户列表
AuthUserFile 

#代表了svn用户对svn访问的权限，比如只读，可写等
AuthzSVNAccessFile
```

这样配置好后下面就要开始创建仓库了

### 创建仓库

进入到 /mnt/sv_repository 目录，比如我想创建一个名字为test的仓库，执行下列命令

```bash
#创建test仓库
svnadmin create test

#更改拥有者为apache
chown -R apache.apache test
```

这样一个仓库就创建好了，然后在创建用户和赋予用户仓库的权限

### 创建svn用户

创建用户需要使用 htpasswd 命令

```bash
htpasswd -c /mnt/svn_repository/svn_user 用户名 用户密码
```

然后打开 /mnt/svn_repository/svn_user 文件，可以看到已经增加了一个用户

### 对仓库赋予用户访问权限

打开 /mnt/svn_repository/svn_user_auth 文件，比如我想对刚才的test仓库使用wutong用户并赋予读写权限，可以这么设置

```bash
[test:/]
wutong=rw
```

### 访问SVN
一切就绪，打开 http://subversion.wutong.me:2048/svn/test 然后输入用户密码就可以访问了

### 增加用户

```bash
htpasswd -b  SVN 用户文件 用户名 密码
```

如：

```bash
htpasswd -b /mnt/svn_repository/svn_user zhangsan 123456
```
