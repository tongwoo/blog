---
layout: post
title: 'PHP类库无法转换PDF的替代方案'
date: 2018-07-11
author: wutong
tags:  linux php pdf
---

在使用php相关类库（基于Imageick）进行转换经常会报错，特别是相关发票，里面包含了一些矢量字体图形之类，经过一番摸索，便使用MuPDF来做处理。

## 安装

访问 [https://mupdf.com/downloads/index.html](https://mupdf.com/downloads/index.html) 下载软件包，下载完成后执行如下命令：

```bash
#解压
tar -xzvf mupdf-1.13.0-source.tar.gz

#编译，编译之前确保相关编译工具已安装
make HAVE_X11=no HAVE_GLUT=no prefix=/usr/local install

#测试转换
mutool convert -F png -o test.png test.pdf

#转换图片的大小（保持比例）
mutool convert -F png -O "width=1500 height=900" -o test.png test.pdf
```

具体命令参考官方文档：[https://mupdf.com/docs/manual-mutool-convert.html](https://mupdf.com/docs/manual-mutool-convert.html)

## 配合PHP

调用 system、passthru、exec 任一函数即可，转换后的文件会自动加上“1”字段，比如想转换成“aaa.png”，那么调用system命令后会变成"aaa1.png"，这是因为PDF有页数。