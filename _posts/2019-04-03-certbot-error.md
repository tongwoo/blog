---
layout: post
title: 'CentOS7 certbot 出错'
date: 2019-04-03
author: wutong
tags:  linux certbot
---

使用仓库的 `certbot` 命令出错，提示无法导入 `ImportError: No module named 'requests.packages.urllib3'` ，用如下命令解决：

```bash
pip install --upgrade --force-reinstall 'requests==2.6.0' urllib3
```