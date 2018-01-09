---
layout: post
title: 'Nginx、Apache的常用功能配置'
date: 2017-12-23
author: wutong
tags:  nginx apache
---


Nginx

### 访问不存在的图片显示默认图片

#### Nginx
```nginx
location ~* \.(jpg|jpeg|gif|png)$ {
    try_files $uri /not-exists.jpg =404;
}
```
#### Apache
```apache
...
```

#### 设置指定文件类型过期时间

#### Nginx
```nginx
location ~* \.(jpg|gif|png|ico|gif|css|js|svg)$ {
    expires 30d;
}

# 其时间单位有如下选项
# ms milliseconds
# s	seconds
# m	minutes
# h	hours
# d	days
# w	weeks
# M	months, 30 days
# y	years, 365 days
```

#### Apache
```apache
ExpiresActive on
ExpiresByType image/jpg "access 1 years"
ExpiresByType image/png "access 1 years"
ExpiresByType image/gif "access 1 years"
ExpiresByType image/jpeg "access 1 years"

# 其时间单位有如下选项
# years
# months
# weeks
# days
# hours
# minutes
# seconds
```
