---
layout: post
title: '安装官方MySQL(CentOS7)'
date: 2019-03-01
author: wutong
tags:  linux mysql
---

系统自带用的 `mariadb` 总感觉是野路子，还是安装官方的吧。

## 下载仓库配置文件

访问 [https://dev.mysql.com/downloads/repo/yum/](https://dev.mysql.com/downloads/repo/yum/) 选择对应的版本并下载保存

安装这个软件包

```bash
yum localinstall 软件包文件路径
```

打开仓库配置文件

```bash
vi /etc/yum.repos.d/mysql-community.repo
```

将需要使用的版本 `enable` 设置为 1，不要的设置为0，默认的是当前最高版本为启用状态

## 安装MySQL

执行命令安装

```bash
yum install mysql-community-server
```

启动

```bash
systemctl start mysqld
```

初始化后下列事情会发生：

 - SSL证书秘钥会生成到data目录
 - 创建了一个 `root` 用户，且密码放到了日志文件中
 
查看密码

```bash
cat /var/log/mysqld.log  | grep password
```

登录MySQL并设置密码

```bash
mysql -u root -p
```

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';
```