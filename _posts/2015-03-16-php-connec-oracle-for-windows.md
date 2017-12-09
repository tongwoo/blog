---
layout: post
title: 'PHP连接Oracle(Windows)'
date: 2015-03-16
author: wutong
tags:  windows php oracle
---

根据需要开启下列扩展

```code
extension=php_oci8.dll
extension=php_oci8_11g.dll
extension=php_pdo_oci.dll
```

这样还不够，还得需要下载 [Instant Client](http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html)

下载之后将其解压目录放入到系统环境变量，如果嫌麻烦就直接解压在 c:\windows 目录

最后，重启apache