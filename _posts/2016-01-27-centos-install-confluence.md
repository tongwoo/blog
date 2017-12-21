---
layout: post
title: 'CentOS 安装 Confluence'
date: 2016-01-27
author: wutong
tags:  linux confluence
---

confluence是个功能非常强大的文档、知识库等管理共享工具，下面是安装的步骤。

### 安装 Java

安装confluence之前必须要把安装 Java 好，首先就要到 [官网下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) rpm安装包并使用 “rpm -ivz 下载的文件名” 命令进行安装，或者直接 yum 安装

 

### 安装 confluence

#### 下载

进入到 [官网下载](https://www.atlassian.com/software/confluence/download-archives) 页面进行下载，这里我选择的是 Confluence 6.1.1 - Standalone (ZIP Archive)，下载下来的文件名是以“zip” 结尾的

#### 安装

##### 路径

下载的文件名为：atlassian-confluence-6.1.1.zip，解压后我放到根目录并且重命名为：confluence，此时的路径

```bash
/confluence
```

建立存放 confluence 数据目录并赋予写入权限

```bash
mkdir /confluence-data
chmod +w /confluence-data
```

修改 /confluence/confluence/WEB-INF/classes/confluence-init.properties 文件，将最后的目录替换成如下目录，注意去掉 # 号

```coce
confluence.home=/web/confluence-data
```

##### MySQL驱动

前往下载 [MySQL官网](https://dev.mysql.com/downloads/connector/j) 下载 Connector/J 驱动 

将解压出来的 mysql-connector-java-5.1.45-bin.jar 文件 复制到如下目录：

```code
/confluence/lib
```
##### 启动Confluence

执行如下命令进行启动

```bash
/confluence/bin/start-confluence.sh
```

访问 http://127.0.0.1:8090 即可按照提示进行安装
 
### 问题

 - 一开始安装正常，重新启动后无法安装并报错
 
 关闭 confluence 并删除 /confluence-data 目录下的所有数据，然后启动 confluence
 
