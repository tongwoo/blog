---
layout: post
title: 'PHP使用SOAP传参的问题'
date: 2015-10-10
author: wutong
tags:  php soap
---

有时候按照官方文档也有可能出错。

使用下面的__soapCall传的参数对方竟然无法接收到

```php
$soap = new SoapClient($url);
$result = $soap->__soapCall("queryRobotStatusCount", [
    "date"=>"2015-08-13"
]);

```

与对方进行联调，最后使用了如下方式解决

```php
$soap = new SoapClient($url);
$result = $soap->queryRobotStatusCount([
    "date"=>"2015-0813"
]);
```