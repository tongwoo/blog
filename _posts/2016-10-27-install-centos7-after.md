---
layout: post
title: '安装完CentOS7之后出现的相关问题'
date: 2016-10-27
author: wutong
tags:  linux centos
---

有时候因为次要版本号的不同总会有一些莫名奇妙的问题，以下是常遇到的问题和解决方法。


### PDO连接 mysql 出现 【SQLSTATE[HY000] [2002] Permission denied】

关闭 selinux 临时关闭敲：“setenforce 0”，永久关闭：/etc/sysconfig/selinux 增加 SELINUX=disabled



## 安装xunsearch无法编译

安装gcc，gcc-c++


### 更改sshd端口不生效

执行下列代码并重启sshd服务，然后防火墙也要加端口

```bash
semanage port -a -t ssh_port_t -p tcp 新的端口号
``` 

### 超级管理员root无法ssh登录

/etc/ssh/sshd_config 文件的 AllowUsers 区块加入 root


### 修改rc.local文件不生效

添加执行权限

```bash
chmod +x /etc/rc.local
```

### 端口无法访问

添加允许端口访问

```bash
#添加80端口
firewall-cmd --add-port=80/tcp --permanent
```