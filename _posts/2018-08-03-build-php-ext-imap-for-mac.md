---
layout: post
title: 'PHP扩展编译之 - IMAP（MacOS）'
date: 2018-08-03
author: wutong
tags:  mac php 
---

Mac下PHP扩展IMAP安装。


## 安装 `iamp-uw`

因为手动编译没成功直接用现成的

```bash
brew install imap-uw 
```

## 安装 `kerberos`

进入网站 [http://web.mit.edu/kerberos/dist/index.html](http://web.mit.edu/kerberos/dist/index.html) 下载源码包，解压后进入src目录执行如下命令

```bash
./configure --prefix=/app/kerberos
make
make install
```

## 编译 `imap` 扩展

下载php源码并进入 `ext/imap` 目录，执行如下命令

```bash
./configure --with-imap-ssl=/usr/local/opt/openssl --with-kerberos=/app/kerberos
make
```

## 安装扩展

将编译后生成的 `ext/imap/modules/imap.so` 复制到Php扩展目录并在php.ini中增加 `extension=imap.so` 即可
