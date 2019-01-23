---
layout: post
title: 'SS新安装'
date: 2019-01-23
author: wutong
tags:  linux
---

安装有变化，记录一下

## MbedTLS

```bash
wget https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/m/mbedtls-2.7.9-1.el7.x86_64.rpm
rpm -Uvh mbedtls-2.7.9-1.el7.x86_64.rpm
wget https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/m/mbedtls-devel-2.7.9-1.el7.x86_64.rpm
rpm -Uvh mbedtls-devel-2.7.9-1.el7.x86_64.rpm
```

## libsodium

```bash
git clone https://github.com/jedisct1/libsodium.git
cd libsodium
./autogen.sh
make
make install
```

## sslibev

```bash
git clone https://github.com/tongwoo/shadowsocks-libev.git
cd shadowsocks-libev
./autogen.sh
make
make install
```

## run

```bash
ss-server -s 0.0.0.0 -p 12345 -k suijimima -a ss -m aes-256-cfb
```