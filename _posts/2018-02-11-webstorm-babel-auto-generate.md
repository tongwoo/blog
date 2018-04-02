---
layout: post
title: '目前前端相关工具和术语解释'
date: 2018-02-11
author: wutong
tags:  nodejs npm webpack javascript babel
---

很长时间没接触前端开发了，因为要做个自己的工具得重拾前端技术，发现现在的前端圈真的是太操蛋了，各式各样的轮子，特整理了一下相关开发工具和说明。

## Babel

### 作用

可以将使用ES6的代码转换成ES5的代码

### 安装

```bash
npm install --save-dev babel-cli babel-preset-env
```

## NPM

### 作用

js的相关库管理工具

### 安装

安装完`nodejs`会自动安装

### Webpack

### 作用

打包、压缩前端资源，如：js,css等

### 安装

```bash
npm install --save-dev webpack
```

## AMD、CMD

### 作用

模块加载的规范

## RequireJS

### 作用

实现了AMD规范动态加载js