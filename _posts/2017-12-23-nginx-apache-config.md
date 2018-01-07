---
layout: post
title: 'Nginx、Apache的常用功能配置'
date: 2017-12-23
author: wutong
tags:  nginx apache
---


### Nginx

访问不存在的图片显示默认图片

```nginx
location ~* \.(jpg|jpeg|gif|png)$ {
    try_files $uri /not-exists.jpg =404;
}
```


### Apache

访问不存在的图片显示默认图片

```apache
...
```
