---
layout: post
title: '安装Shadowsocks服务端'
date: 2015-11-14
author: wutong
tags:  linux shadowsocks
---

在不翻墙的情况下访问某些站点无法打开或者很慢，所以只能挂代理。
但是，购买的代理不稳定，所以最好的方法就是自己花钱自己搭建代理
服务器。

## CentOS下的安装

### 安装

```bash
yum install python-setuptools && easy_install pip
pip install shadowsocks
```
### 命令行启动

```bash
#默认启动无密码，端口 8838，加密方式为 aes-256-cfb
ssserver -d start
```

### 使用配置文件启动

创建 /etc/shadowsocks/config.json 并填入如下参数

```json
{
    "server":"104.214.138.102",
    "server_port":443,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"mima",
    "timeout":600,
    "method":"aes-256-cfb"
}
```

执行启动命令

```bash
ssserver -c /etc/shadowsocks/config.json -d start
```

执行关闭命令

```bash
ssserver -c /etc/shadowsocks/config.json -d stop
```
