---
layout: post
title: '隐藏响应头中的敏感信息'
date: 2014-08-12
author: wutong
tags:  linux php mysql mariadb apache
---

在响应头中暴露出来的web服务器版本、PHP版本有潜在的安全性，隐藏它。

### php.ini

```ini
expose_php = Off
```

### httpd.conf

```apacheconf
ServerSignature Off
ServerTokens Prod
```

### nginx.conf

```nginx
server_tokens off;
```