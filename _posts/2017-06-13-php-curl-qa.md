---
layout: post
title: 'PHP的CURL扩展和相关SSL知识点'
date: 2017-06-13
author: wutong
tags:  php ssl
---

一些自己整理的问答。

### 为什么php调用curl库连接https站点的时候报错说无法验证证书？

php的curl库默认不信任任何证书，所以请求https站点的时候需要指定一个证书

### php的curl请求https需要的证书如何获得？

访问 https://curl.haxx.se/docs/caextract.html 下载pem格式的证书即可，这是一个根证书的集合，从mozilla中导出来的，包含了大部分的信任的根证书

### php的curl请求https为什么需要本地的证书？

因为访问的htpps站点的证书肯定是其他CA机构颁发的，本地的根证书来验证站点的证书是否正常

### charles为什么要要求安装他们的根证书？

charles的根证书用来冒用客户端的请求和服务端的响应从而达到代理的效果，前提是应用或者浏览器要信任charles的根证书