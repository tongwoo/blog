---
layout: post
title: 'Gitlab安装'
date: 2018-03-06
author: wutong
tags:  linux php mysql mariadb apache
cover: '/assets/img/hero.jpg'
---

看了看办公室的古董服务器放在那里没什么用，就当git仓库来用好了，刚好4G内存。


### 下载

访问 [https://about.gitlab.com/installation](https://about.gitlab.com/installation) 点击对应的系统。

### 环境准备

古董装的是 `CentOS7`，先把准备工作做好，如果下方的操作已经之前做过了则忽略即可，另外 gitlab 安装包集成了 nginx、postsql、redis之类的工具，所以也要确保端口没被占用，如果占用了则安装gitlab之后修改配置文件。

**允许防火墙开放http协议、启用SSH之类的操作

```bash
sudo yum install -y curl policycoreutils-python openssh-server
sudo systemctl enable sshd
sudo systemctl start sshd
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
```

继续

```bash
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
```

### 添加gitlab仓库并安装

```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash
```

### 绑定域名

将下方的域名换成自己的域名，或者编辑 `/etc/gitlab/gitlab.rb` 文件，找到
```bash
sudo EXTERNAL_URL="http://gitlab.example.com" yum install -y gitlab-ee
```

未完待续