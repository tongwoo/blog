---
layout: post
title: 'PHP远程调试'
date: 2018-07-01
author: wutong
tags:  linux php
---

有时候在线上环境可能出现的bug不能随便的添加代码来处理，利用远程调试可快速定位bug

### 远程调试

调试之前确定如下软件或扩展已装好

- phpStorm
- xdebug
- 路由器管理权限

### XDEBUG配置

注意这里的XDEBUG配置是指服务器上的配置，而不是你本机的配置。

```ini
;是否启用调试（必须开启）
xdebug.default_enable = On
;是否将调试请求转发到当前的调试者（访问者，必须开启）
xdebug.remote_connect_back = On
;调试者的端口（开发人员的本机端口，必须填写）
xdebug.remote_port = 5000
;是否启用远程调试（必须开启）
xdebug.remote_enable = On
;是否在浏览者访问的时候自动触发调试，如果为0则只有设
;置了XDEBUG_SESSION给cookie的时候才会触发，视情况
;而定。如果是自己在浏览器中进行调试的话可以设为0，如
;果是类似微信回调请求调试的话则设为1，因为微信回调是
;直接服务器发送给服务器，没法设置XDEBUG_SESSION
xdebug.remote_autostart=1
;远程调试人员的机器IP，视情况填写，一般不填写
xdebug.remote_host=156.35.12.35
```

### phpStorm配置

将phpstorm中的端口填写为xdebug配置中的端口，配置截图：
![端口](/screenshot/2018-07-01/xdebug-phpstorm.png)
在phpstorm中建立一个调试主机并设置本机目录与服务器目录映射，配置截图：
![映射](/screenshot/2018-07-01/xdebug-phpstorm-server.png)

### 路由器设置

当调试的时候xdebug会把调试请求`主动` 发送到配置的端口，因为默认路由器不转发外部端口到本机，所以需要在路由器里把端口转发到本机上，设置截图：
![路由器](/screenshot/2018-07-01/xdebug-router.png)


### 开始调试

如果开启了 `xdebug.remote_autostart` 则直接浏览网页即可触发调试请求，如果未开启则手动点击phpstorm上的调试按钮或者安装google插件[xdebug](https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc)，演示效果：

![调试效果](/screenshot/2018-07-01/xdebug-demo.gif)
