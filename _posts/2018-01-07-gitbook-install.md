---
layout: post
title: 'Gitbook 的安装与使用'
date: 2018-01-07$
author: wutong
tags:  git gitbook
---

Gitbook是一个可以使用markdown来撰写并利用github存储然后生成一本电子书的应用，不过我们也可以用他来做其他用途，比如开发文档。

### 安装客户端

用npm命令来进行安装

```bash
npm install -g gitbook-cli
```

安装完成之后，我们可以用 `gitbook` 命令来生成电子书。

### 写文章

#### 初始化
使用 `gitbook init [book]` 初始化一个项目，比如：

```bash
gitbook init booktest
```

则创建了如下文件：

```code
booktest/
├── README.md
└── SUMMARY.md
```

其中 `SUMMARY.md` 就是目录文件

#### 电子书配置
还可以建立一个配置文件 `book.json`

```json
{
    "gitbook": "版本",
    "title": "书名",
    "description": "介绍",
    "language": "zh",
    "structure": {
      "readme": "README.md"
    },
    "pluginsConfig": {
        "fontSettings": {
            "theme": "white",
            "family": "msyh",
            "size": 2
        },
        "plugins": [
            "插件名称"
        ]
    }
}
```
#### 设置文章目录

编辑 `SUMMARY.md` 文件

```markdown
* [1.文章标题](链接的页面)
* [2.PHP的入门与精通](php.md)
    * [2-1.子目录](php_child.md)
    * [2-2.第1章](chapter1.md)
```

#### 生成电子书

输入如下代码即可生成默认的HTML格式电子书

```bash
gitbook build
```
生成过程
```bash
info: 7 plugins are installed
info: 6 explicitly listed
info: loading plugin "highlight"... OK
info: loading plugin "search"... OK
info: loading plugin "lunr"... OK
info: loading plugin "sharing"... OK
info: loading plugin "fontsettings"... OK
info: loading plugin "theme-default"... OK
info: found 1 pages
info: found 0 asset files
info: >> generation finished with success in 0.5s !
```
会出现一个 `_book` 的目录，打开 `index.html` 预览