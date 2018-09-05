---
layout: post
title: '安装Ngrok服务端和客户端'
date: 2017-12-21
author: wutong
tags:  linux ngrok
---

ngrok是个不错的http内网转发应用。


### 安装

安装Go

```bash
yum -y install golang
```

克隆ngrok git仓库

```bash
git clone "https://github.com/tongwoo/ngrok.git"
cd ngrok
```

根据环境进行编译

```bash
#服务端
make release-server

#客户端
make release-client
```

### 配置及启动

服务端启动

```bash
#为了方便直接测试，设置成如下端口并启动
./ngrokd -domain ngrok.wutong.me -httpAddr ":4001" -httpsAddr ":4032" -tunnelAddr ":6023"
```

因为默认80端口被nginx使用，所以做个转发，建立如下的 conf 文件并重新启动nginx

```nginx
server {
    listen 80;
    server_name ngrok.wutong.me *.ngrok.wutong.me;
    error_log /logs/ngrok_error.log;
    access_log /logs/ngrok_access.log main;
    location / {
        proxy_pass http://127.0.0.1:2001/;
        proxy_redirect off;
        proxy_set_header Host $host:2001;
    }
}
```

客户端连接

创建一个 config.yml 文件放到ngrok同目录，并填充如下内容

```yml
#代表服务器的隧道地址和端口
server_addr: "ngrok.wutong.me:6003"
```

客户端启动

```bash
# 以 lala.ngrok.wutong.me 来作为访问者访问的域名
ngrok -config=./config.yml -subdomain=lala 80
```

启动成功

```code
Tunnel Status                 online
Version                       1.7/1.7
Forwarding                    https://lala.ngrok.wutong.me:2001 -> 127.0.0.1:80
Forwarding                    http://lala.ngrok.wutong.me:2001 -> 127.0.0.1:80
Web Interface                 127.0.0.1:4040
# Conn                        0
Avg Conn Time                 0.00ms
```

### 浏览

访问 http://lala.ngrok.wutong.me 即可看到网页的内容已经映射到本机上了。