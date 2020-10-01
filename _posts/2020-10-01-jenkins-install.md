---
layout: post
title: 'Jenkins配置hook'
date: 2020-10-01
author: wutong
tags:  Jenkins
---

之前用的都是 `Poll SCM` 模式，为了不想每次都要等那么一会儿，改成提交代码后就自动打包发布，记录一下

**一、安装 Build Authorization Token Root 插件**

进入 `Manage Jenkins` - `Plugin Manager` - `Available` 中搜索 `Build Authorization Token Root` 并安装

**二、配置Pipeline**

新建一个 `Pipeline`，在 `Build Triggers` 选项卡中选中 `Trigger builds remotely` 并自己写个 `token` 

**三、配置Web hook**

我用的是 `coding`，所以打开 `项目设置` - `开发者选项` - `Web Hook` 中新增一个钩子，钩子的 `URL` 填写格式如下

```
格式：Jenkins地址+buildByToken/build?job=创建的Pipeline名称&token=上面配置的token
例子：http://jenkins.wutong.me/buildByToken/build?job=test&token=wutong
```

**四、测试**

手动执行 `curl http://jenkins.wutong.me/buildByToken/build?job=test&token=wutong` 是否成功

**403错误**

如果遇到403错误，则进入 `Manage Jenkins` -  `Configure Global Security` - `CSRF Protection` 后选中 `Enable proxy compatibility` 选项并保存
