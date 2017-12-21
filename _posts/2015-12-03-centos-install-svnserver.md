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

安装完成后会在 /etc/httpd/conf.d 或者 /etc/httpd/conf.modules.d 目录生成一个 subversion.conf 配置文件，更改里面的配置

```bash
#用于连接的端口号
Listen 4096
<VirtualHost *:4096>
    ServerName svn.com
    #用浏览器浏览的时候不显示目录结构
    Options -Indexes
    <Location /svn>
        DAV svn
        # svn仓库目录
        SVNParentPath /svn/repository
        AuthType Basic
        # 连接svn的欢迎信息
        AuthName "Welcome to wutong's SVN server."
        # svn用户列表
        AuthUserFile /svn/user
        # svn用户授权列表，代表了svn用户对svn访问的权限，比如只读，可写等
        AuthzSVNAccessFile /svn/user_auth
        Require valid-user
    </Location>
</VirtualHost>
```

这样配置好后下面就要开始创建仓库了

### 创建仓库

进入到 /svn/repository 目录，比如我想创建一个名字为test的仓库，执行下列命令

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
htpasswd -b /svn/user 用户名 用户密码
```

然后打开 /svn/user 文件，可以看到已经增加了一个用户

### 对仓库赋予用户访问权限

打开 /svn/user_auth 文件，比如我想对刚才的test仓库使用wutong用户并赋予读写权限，可以这么设置

```bash
[test:/]
wutong=rw
```

### 访问SVN

一切就绪，打开 http://svn.com:2048/svn/test 然后输入用户密码就可以访问了

