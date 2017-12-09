---
layout: post
title: 'PHP配置DB2(windows)'
date: 2015-10-08
author: wutong
tags:  windows php db2
---

供电局的系统用的DB2，不给接口直接给数据库的操作权限，想想也是醉了，废话不多说，下面是我的配置DB2扩展的过程（仅限windows）

### 前言

扩展的使用跟PHP的版本息息相关，下面是我使用的软件或运行库，安装好后重启web服务器并查看phpinfo()是否有db2的扩展选项

### PHP5.5 VC11 x86 Thread Safe

下载地址： http://windows.php.net/download#php-5.5

### 使用此PHP版本需要VC11运行库

下载地址： http://www.microsoft.com/en-us/download/details.aspx?id=30679

### 下载与PHP版本对应的DB2扩展

下载地址： http://pecl.php.net/package/ibm_db2

还得需要DB2CLI（ibm_data_server_driver_package）下载与系统对应的版本

下载地址： http://www-01.ibm.com/support/docview.wss?uid=swg24040536

最后在PHP.INI增加扩展选项

```code
extension=php_ibm_db2.dll
```

### 连接测试

```php
//数据库名
$dbName = "PWYWTEST";
//数据库用户名
$dbUser = "db2admin";
//数据库密码
$dbPassword = "*****";
//连接字符串
$dbConn = "DRIVER={IBM DB2 ODBC DRIVER};DATABASE=$dbName;" .
    "HOSTNAME=127.0.0.1;PORT=50000;PROTOCOL=TCPIP;UID=$dbUser;PWD=$dbPassword;";
//测试连接
$conn = db2_connect($dbConn, "", "");
if ($conn) {
    echo "suucess";
}else{
    echo "fail";
}
//线路重载
$sql = "SELECT * FROM userpd.T_PD_YWZHZBB_PWFH";
//执行结果
$executeResult=db2_exec($conn,$sql);
//获取当前行的结果集
$result=db2_fetch_assoc($executeResult)
//输出
var_dump($result);
```