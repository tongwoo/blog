---
layout: post
title: '升级到MacOS后，SSH无法自动登录了'
date: 2017-07-24
author: wutong
tags:  mac ssh
---

升级到最新的MacOS之后，之前SSH自动登录老是要求输入密码。

```bash
vi ~/.ssh/config

#输入下列代码
UseKeychain yes
```