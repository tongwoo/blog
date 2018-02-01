---
layout: post
title: 'Mac升级到10.13连接SSH每次都要输入密码'
date: 2018-01-25$
author: wutong
tags:  mac ssh
---

编辑 `~/.ssh/config` 并输入如下代码

```bash
UseKeychain yes 
AddKeysToAgent yes 
```