---
layout: post
title: 'PHP中socket读写的超时设置'
date: 2017-10-11
author: wutong
tags:  php
---

介绍如何设置超时时间的方法。

```php
//读超时
socket_set_option($client, SOL_SOCKET, SO_RCVTIMEO, [
    'sec'=>8,
    'usec'=>0,
]);
//写超时
socket_set_option($client, SOL_SOCKET, SO_SNDTIMEO, [
    'sec'=>8,
    'usec'=>0,
]);
```