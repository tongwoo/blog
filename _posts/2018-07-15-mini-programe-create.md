---
layout: post
title: '小程序快速创建page'
date: 2018-07-15
author: wutong
tags:  linux php 
---

在开发小程序中会经常创建 page,创建一个page文件夹不够，还得再创建同名的 js、json、wxml、wxss，很费事儿，用python写个脚本一劳永逸了。


代码保存为`minitool` 并加入到环境变量，输入 'minitool create page名称' 即可创建完成，代码：

```python
#!/usr/bin/env python

import sys
import os
from os import path

# 参数列表
args = sys.argv[1:]

# 没有参数
if len(args) == 0:
    print('need command argument.')
    exit()

# 命令
cmd = args[0]

# 命令列表
commands = ['create']
if cmd not in commands:
    print('the command invalid.')
    exit()


def get_tpl_content(ext):
    script_path = path.dirname(__file__)
    tpl_file = script_path + os.sep + 'templates' + os.sep + ext + '.' + ext
    if not path.exists(tpl_file):
        return ''
    fp = open(tpl_file, 'r')
    content = fp.read()
    fp.close()
    return content


# 命令 - 创建文件
if cmd == 'create':
    if len(args) != 2:
        print('the create command argument invalid.')
        exit()

    # 要创建的文件名称
    fpath = path.relpath(args[1])
    if not path.exists(fpath):
        try:
            os.makedirs(fpath)
        except IOError as e:
            print('can\'t create folder：' + e.args[1])
            exit()
    basename = fpath.split(os.sep)[-1]
    exts = ('js', 'json', 'wxml', 'wxss')
    for ext in exts:
        file = fpath + os.sep + basename + '.' + ext
        if path.exists(file):
            continue
        fp = open(file, 'w')
        # 使用模板
        # content = get_tpl_content(ext)
        content = 'test'
        fp.write(content)
        fp.close()
        print('the file \'' + file + '\' created.')

```