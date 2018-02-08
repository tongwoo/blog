---
layout: post
title: '编译PHP7的intl扩展'
date: 2018-02-09
author: wutong
tags:  linux php intl icu
---

为了能获得 `intl.so` 这个文件，我熬了2个晚上到2，3点，一言难进，下面说说过程。


### 起因

在一个Yii项目中进行流式下载文件的时候会抛出如下错误：

```code
Error: transliterator_transliterate(): 
Could not create transliterator with ID &quot;Any-Latin;Latin-ASCII; [\u0080-\uffff] remove&quot; (transliterator_create: unable to open ICU transliterator with id &quot;Any-Latin; Latin-ASCII; [\u0080-\uffff] remove&quot;: U_INVALID_ID)
```

不太明白为什么跟国际化的函数有关系，经过跟踪调试，觉得测试服务器的模块可能版本较低，于是执行了 `php -f requirements.php` 来检查环境是否满足，输出如下：

```code
.......

OpenSSL extension: OK

Intl extension: OK

ICU version: WARNING!!!
Required by: Internationalization support
Memo: ICU 49.0 or higher is required when you want to use # placeholder in plural rules
        (for example, plural in

        Formatter::asRelativeTime()) in the yii\i18n\Formatter class. Your current ICU version is 4.2.1.

ICU Data version: WARNING!!!
Required by: Internationalization support
Memo: ICU Data 49.1 or higher is required when you want to use # placeholder in plural rules
        (for example, plural in

        Formatter::asRelativeTime()) in the yii\i18n\Formatter class. Your current ICU Data version is (ICU Data is missing).

Fileinfo extension: OK

DOM extension: OK

......

Expose PHP: WARNING!!!
Required by: Security reasons
Memo: "expose_php" should be disabled at php.ini

PHP allow url include: OK

PHP mail SMTP: OK

------------------------------------------
Errors: 0   Warnings: 4   Total checks: 24
```

可以看到 `ICU` 这个库版本太低了，需要 `49` 版本才行，于是开始升级 `ICU`


### 升级ICU过程

运行 `yum info icu` 得知版本是 `4.2`

```code
Name        : icu
Arch        : x86_64
Version     : 4.2.1
Release     : 14.el6
Size        : 167 k
Repo        : base
Summary     : International Components for Unicode
URL         : http://www.icu-project.org/
License     : MIT and UCD and Public Domain
Description : Tools and utilities for developing with icu.
```
#### 获取新的ICU包

前往 [http://site.icu-project.org/download](http://site.icu-project.org/download) 下载所需要的版本，我选择的是 `49.1`，为了方便我直接选择了编译好的版本 `icu4c-49_1_2-RHEL6-i386.tgz` ，执行如下命令解压并将解压后的目录结构移动到根目录

```bash
tar xzf icu4c-49_1_2-RHEL6-i386.tgz
mv -r ./usr/ /
```

#### 升级intl

因为之前的 `intl` 扩展是按照旧的版本`icu`编译的，所以我一开始想要升级，于是直接执行 `pecl upgrade intl`，报如下错误：

```code
downloading intl-3.0.0.tgz ...
Starting to download intl-3.0.0.tgz (248,200 bytes)
....................................................done: 248,200 bytes
150 source files, building
running: phpize
Configuring for:
PHP Api Version:         20160303
Zend Module Api No:      20160303
Zend Extension Api No:   320160303
Specify where ICU libraries and headers can be found [DEFAULT] :
building in /var/tmp/pear-build-rootYIUFQ9/intl-3.0.0
running: /var/tmp/intl/configure --with-php-config=/usr/bin/php-config --with-icu-dir=DEFAULT
checking for grep that handles long lines and -e... /bin/grep

......

在包含自 /var/tmp/intl/php_intl.h：34 的文件中，
                 从 /var/tmp/intl/php_intl.c：25:
/var/tmp/intl/intl_error.h:24:40: 错误：ext/standard/php_smart_str.h：没有那个文件或目录
make: *** [php_intl.lo] 错误 1
ERROR: `make' failed
```

经过百度得知在 `php7` 开始后 `ext/standard/php_smart_str.h` 文件已经变为 `ext/standard/php_smart_str.h` 于是天真的改了源代码的文件名，还是报错。

**若干时间后……**

得知 `intl` 扩展已经迁移到官方源代码中，于是 `git clone 当前php版本` 的源代码到服务器，删除之前装的 `intl` 扩展。

进入克隆之后的代码目录执行：

```bash
#进入扩展目录
cd php-src-PHP-7.1.13/ext/intl

#phpize
[root@xxx intl]# phpize
Configuring for:
PHP Api Version:         20160303
Zend Module Api No:      20160303
Zend Extension Api No:   320160303

#编译配置
./configure

#编译
make
```

经过漫长的时间等待之后，出现了成功画面：

```code

----------------------------------------------------------------------
Libraries have been installed in:
   /tmp/php-src-PHP-7.1.13/ext/intl/modules

If you ever happen to want to link against installed libraries
in a given directory, LIBDIR, you must either use libtool, and
specify the full pathname of the library, or use the `-LLIBDIR'
flag during linking and do at least one of the following:
   - add LIBDIR to the `LD_LIBRARY_PATH' environment variable
     during execution
   - add LIBDIR to the `LD_RUN_PATH' environment variable
     during linking
   - use the `-Wl,-rpath -Wl,LIBDIR' linker flag
   - have your system administrator add LIBDIR to `/etc/ld.so.conf'

See any operating system documentation about shared libraries for
more information, such as the ld(1) and ld.so(8) manual pages.
----------------------------------------------------------------------

Build complete.
Don't forget to run 'make test'.
```
将 `modules/intl.so` 文件拷贝到 php 的扩展目录并启用即可

至此，此更新终于完成