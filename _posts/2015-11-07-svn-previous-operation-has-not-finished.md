---
layout: post
title: 'SVN出现Previous operation has not finished'
date: 2015-11-07
author: wutong
tags:  svn
---

很诡异的一个问题。

### 问题
今天在进行cleanup的时候出现“Previous operation has not finished; run ‘cleanup’ if it was interrupted”这样的错误，这是因为以前可能提交的时候中断了

### 解决方法
打开 根目录下的“.svn” 目录，使用sqlite管理工具打开“wc.db”，然后删除表 “WORK_QUEUE” 里的内容