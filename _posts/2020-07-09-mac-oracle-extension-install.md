---
layout: post
title: 'MacOS安装Oracle驱动与PHP oci8扩展'
date: 2020-07-09
author: wutong
tags:  oracle
---


项目需要进行Oracle数据使用，本文记录了如何在MacOS系统下进行Oracle驱动和PHP oci8的扩展

## 下载

下载页面：

[https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html]()

需要下载如下2个压缩包：

 - Basic Package
 - SDK Package
 
下载后将2个压缩包进行解压并将SDK压缩包里的sdk文件夹复制到Basic文件夹


## 链接

链接的目的是让驱动能被其他开发工具或软件能找到驱动目录

假设上面的解压后的文件夹为 `/extensions`，则执行如下命令

```
ln -s /extensions/libclntsh.dylib /usr/local/lib/
```

执行后依赖此驱动的工具软件可开始连接oracle数据库

## 安装oci8

执行如下命令

```
pecl install oci8
```

提示出现如下文字

```
running: phpize
Configuring for:
PHP Api Version:         20180731
Zend Module Api No:      20180731
Zend Extension Api No:   320180731
Please provide the path to the ORACLE_HOME directory. Use 'instantclient,/path/to/instant/client/lib' if you're compiling with Oracle Instant Client [autodetect] :
```

则输入上文中设置的目录 `instantclient,/extensions`，确保SDK文件夹也在此目录，稍等片刻后即可编译成功且自动加入`php.ini`

执行 `php -m` 可查看扩展是否载入成功


