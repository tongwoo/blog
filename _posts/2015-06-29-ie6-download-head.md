---
layout: post
title: 'IE6下载需要这样的格式'
date: 2015-06-29
author: wutong
tags:  ie6 php
---

在IE6浏览器提示下载会出现乱码或者无法找到文件。


可以尝试加入下列代码来实现IE6正常的下载

```php
ob_clean();
header("ontent-type:application/media");
header("cache-control: must-revalidate, post-check=0, pre-check=0");
header("pragma: public");
header("content-disposition:attachment;filename=呵呵.mp4");
echo file_get_contents($path);
```


