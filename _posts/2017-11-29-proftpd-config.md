---
layout: post
title: '采用MySQL认证的Proftpd安装与配置'
date: 2017-11-29
author: wutong
categories: 技术
tags:  proftpd mysql
---

虽然SVN更新代码很方便，但是有的时候的情况下不得不使用FTP来上传文件，这个时候就需要一个FTP服务端来处理了，
本篇文章即是达到这个目的。

## 环境

CentOS 6，其他差不多

## 安装
```bash
yum install proftpd proftpd-mysql
```

## 配置

#### 配置文件

安装后的配置文件路径：/etc/proftpd.conf

打开配置文件，注释掉如下2行不启用

```apacheconf
AuthPAMConfig       proftpd
AuthOrder           mod_auth_pam.c* mod_auth_unix.c
```

再取消如下几行的注释并启用

```apacheconf
LoadModule mod_sql.c
LoadModule mod_sql_passwd.c
LoadModule mod_sql_mysql.c
```

增加MYSQL的认证授权方式

```apacheconf
#检查用户或者用户组
SQLAuthenticate users groups
#类型为明文密码
SQLAuthTypes Plaintext
#数据库为MYSQL
SQLBackend mysql
#FTP连接成功后的默认目录（如果数据库里没填的话）
SQLDefaultHomedir /ftpfolder
#MYSQL数据库连接信息,格式：数据库名@主机地址:端口号 用户名 密码
SQLConnectInfo ftp@127.0.0.1:3306 ftpuser ftpuser
#SQL日志
SQLLogFile /var/log/proftpd/sql.log
#最小的UID,GID，这个到时候是和系统的用户进行对应的，我这里
#用户的是apache，因为我要直接管理web站点
SQLMinID 40
```

增加日志记录

```apacheconf
ExtendedLog /var/log/proftpd/ftp.log ALL
SystemLog /var/log/proftpd/sys.log
ServerLog /var/log/proftpd/server.log
```

增加虚拟目录的符号链接的支持

```apacheconf
VRootOptions allowSymlinks
```

我这里想直接管理web目录，所以最好的方式是使用apache用户和apache的组，输入如下命令查看apache的用户、组的UID、GID得知分别是48、48，记录下来备用

```bash
[root@wz html]# cat /etc/passwd | grep apache
apache:x:48:48:Apache:/var/www:/sbin/nologin
[root@wz html]# cat /etc/group | grep apache
apache:x:48:
```

将配置文件的User和Group分别改成apache

```apacheconf
User       apache
Group      apache
```

#### 数据库配置

运行如下的SQL语句建立 users、groups 表，注意：users没加uid的唯一索引，意味着不同的用户可以使用同样的uid，即同样的apache用户

```sql
CREATE TABLE `users` (
  `userid` varchar(30) NOT NULL,
  `passwd` varchar(80) NOT NULL,
  `uid` int(11) DEFAULT NULL,
  `gid` int(11) DEFAULT NULL,
  `homedir` varchar(255) DEFAULT NULL,
  `shell` varchar(255) DEFAULT NULL,
  UNIQUE KEY `userid` (`userid`),
  KEY `users_userid_idx` (`userid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

```sql
CREATE TABLE `groups` (
  `groupname` varchar(30) NOT NULL,
  `gid` int(11) NOT NULL,
  `members` varchar(255) DEFAULT NULL,
  KEY `groups_gid_idx` (`gid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

增加个一个测试用户试试

```sql
INSERT INTO users(userid,passwd,uid,gid)VALUES("xiaowu","mima",48,48);
```

使用FTP客户端连接测试成功，如果登录失败请查看 /var/log/proftpd/server.log 日志的提示


## 增加虚拟目录的支持

我这里的实现方式是创建一个软连接，比如我想把 /var/www/html/system 映射到我的FTP根目录，则执行如下命令

```bash
ln -s /var/www/html/system /ftpfolder/测试系统
```

这个时候在FTP客户端里即可看到“测试系统”的一个文件夹，如果没有显示则是当前用户没有这个文件夹的权限

## 目录权限

增加如下配置端可实现不用用户、组的控制权限

```apacheconf
<Directory "/目录全路径">
    <Limit ALL>
        AllowGroup OR 用户组,用户组2
        DenyAll
    </Limit>
</Directory>
```

比如想让 /web 只有 phper 用户组才有写入的权限：

```apacheconf
<Directory "/web">
    <Limit WRITE>
        AllowGroup phper
        DenyAll
    </Limit>
</Directory>
```
这个时候 groups、users 表的数据为：


| groupname | gid | members |
| --- | --- | --- |
| phper | 1000 | tony,alice |


| userid | passwd | uid | gid | homedir | shell |
| --- | --- | --- | --- | --- | --- |
| tony | tony | 1000 | 1000 | null | null |
| alice | alice | 1000 | 1000 | null | null |


比如想让 /web 只有 phper或者javaer 用户组才有写入的权限：

```apacheconf
<Directory "/web">
    <Limit WRITE>
        AllowGroup OR phper,javaer
        DenyAll
    </Limit>
</Directory>
```
这个时候 groups、users 表的数据为：


| groupname | gid | members |
| --- | --- | --- |
| phper | 1000 | tony,alice |
| javaer | 1000 | tony,mei |


| userid | passwd | uid | gid | homedir | shell |
| --- | --- | --- | --- | --- | --- |
| tony | tony | 1000 | 1000 | null | null |
| alice | alice | 1000 | 1000 | null | null |
| mei | mei | 1000 | 1000 | null | null |


注意：路径必须为FTP客户端呈现的路径而不是系统上的路径


## 常见问题

### 1、设置的 Directory 路径参数不生效
 
 路径必须为FTP客户端呈现的路径而不是系统上的路径
 
### 2、设置的链接目录看不见

 FTP用户没有这个目录的权限
 
### 3、无法连接到FTP服务器

 检查服务器21端口是否在防火墙的入站白名单
 
### 4、用Mac系统的FTP客户端能连接管理文件，但Windows下的FTP客户端不行

 粗暴方法：关闭服务端的防火墙