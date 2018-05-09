---
layout: post
title: '升级OpenSSH'
date: 2018-05-09
author: wutong
tags:  linux openssh
---

安装过程有点坑


### 准备工作

安装TelnetServer以便万一原先的ssh无法登录

[安装方法](/install-telnet-server)

安装开发工具

```bash
yum groupinstall 开发工具
```

获取最新的OpenSSH安装包

```
#下载
wget "https://openbsd.hk/pub/OpenBSD/OpenSSH/portable/openssh-7.7p1.tar.gz"
#解压
tar -xzf openssh-7.7p1.tar.gz
```

卸载原先的OpenSSH

```
yum remove openssh
```

如果出现有很多不必要的依赖也卸载的话，则改为手动卸载

```
rpm -e --nodeps openssh
rpm -e --nodeps openssh-clients
rpm -e --nodeps openssh-server
```

## 安装工作

进入刚才解压的 openssh-7.7p1 目录，执行如下命令，如果提示相关c文件不存在，则安装相关开发包，如：openssl-devel

```
cd /tmp/openssh-7.7p1
#指定安装目录为/app/openssh77
./configure -prefix=/app/openssh77
make
make install
```

完善openssh开机脚本

```
#拷贝脚本文件
cp /tmp/openssh-7.7p1/contrib/redhat/sshd.init /etc/init.d/sshd
#修改里面的相关路径为 /app/openssh77
vim /etc/init.d/sshd
#设置为自启动
chkconfig sshd on
```

## 安装完毕

重启机器确认开机脚本是否正常启动，如果正常启动则关闭 telnet 服务

```
service xinetd stop
```