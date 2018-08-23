---
layout: post
title: 'Nginx、Apache+PHP 实现图片自动缩略图'
date: 2018-08-23
author: wutong
tags:  php nginx apache
---

在使用第三方存储的时候，第三方提供商会提供「图片样式」的功能来实现图片扩展名加上样式名随意改变原始图片的体积，考虑到一开始请求量不是很多，可以自己实现这个功能，等量上来了直接上CDN。

### 定义样式规则

假如 `http://img.domain.com/test.jpg` 是一张原始图片，我们想要在后面加上 `-small` 来实现最小图片的功能，`-medium` 来实现图片中等缩放的功能，那么只要重写这些 `URL` 并发送给php来处理进行缩放即可。

### 重写 - Nginx

```nginx
#在 server 区块里加入如下配置代码：
rewrite (.+)\.(jpg|jpeg|png)\-(mini|low|medium|high|ultra|extreme)$ $1.$2.$3.$2 last;	
location ~* \.(jpg|jpeg|png)$ {
    if ( !-f $request_filename ) {
        rewrite . /image-handler.php?path=$document_uri last;
    }
}
```

### 重写 - Apache

```apacheconfig
#在资源目录新建一个 .htaccess 文件并加入如下代码

RewriteEngine On

RewriteRule (.+)\.(jpg|jpeg|png)\-(mini|low|medium|high|ultra|extreme)$ $1.$2.$3.$2 [N]

RewriteCond %{REQUEST_FILENAME} \.(jpg|jpeg|png)$
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule (.+\.(jpg|jpeg|png))$ /image-handler.php?path=$1 [L]
```

### PHP

在上文中的 `image-handler.php` 是处理图片缩放用，其代码可自行实现，`path` 是请求的图片路径，可以根据这个路径来对原图进行缩放。

### 后续

如果不想在资源目录放入这些文件，则可直接加入软连接链接到这个位置。