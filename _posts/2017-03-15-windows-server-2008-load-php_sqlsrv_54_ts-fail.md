---
layout: post
title: 'Windows server 2008 无法加载php_sqlsrv_54_ts.dll'
date: 2015-03-16
author: wutong
tags:  windows php sqlserver
---
sqlsrv是微软的官方扩展，不过在使用的时候可能会遇到无法加载的情况。


首先是在输出的phpinfo()页面中查看，如果没有那么就说明没有加载，确认以下几种情况是否存在

### 可能情况

 - 是否在 php.ini 中添加了 extension=php_sqlsrv_54_ts.dll
 - php.ini 中的 extension_dir目录是否正确
 - extension_dir 目录是否有php_sqlsrv_54_ts.dll
 - 双击 php.exe 看是否有错误提示，如果有 “缺少msvcp100.dll”，请安装 vc2010运行库，注意：要安装32位版的
 - 下载的 sqlsrv 是否符合当前系统，注意甄别！详细条件需要查看手册里面说明
 - 以上的更改后是否重启了 apache 或者其他web服务器

### php_sqlsrv_54_ts.dll扩展下载地址：

[http://sqlsrvphp.codeplex.com/releases/view/85767](http://sqlsrvphp.codeplex.com/releases/view/85767)

 

### 最后

如果在使用php进行连接的时候，还得需要安装 Microsoft SQL Server Native Client（根据系统选择32或者64位安装）