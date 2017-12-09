---
layout: post
title: 'iTerm色彩方案'
date: 2015-12-15
author: wutong
tags:  iterm
---

默认的一团绿色很丑。


打开 ~/.bash_profile 文件，没有就创建，输入下列代码

```bash
export CLICOLOR=1
export LSCOLORS=GxFxCxDxBxegedabagaced
export PS1='[\033[01;32m]u@h[\033[00m]:[\033[01;34m]w[\033[00m]$'
```

然后打开iterm，切换到 colors 选项卡，载入一个喜欢的主题，如果没有可以到 [https://github.com/baskerville/iTerm-2-Color-Themes](https://github.com/baskerville/iTerm-2-Color-Themes) 上下载，然后使用iterm导入即可