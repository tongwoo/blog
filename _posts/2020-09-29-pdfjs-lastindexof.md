---
layout: post
title: 'PDFJS相关问题'
date: 2020-09-29
author: wutong
tags:  pdf js
---

在使用 `PDFJS` 的时候，遇到一些问题，下面是问题和解决方式。

# 在哪里下载PDFJS文件？

访问：[http://mozilla.github.io/pdf.js/getting_started/#download](http://mozilla.github.io/pdf.js/getting_started/#download) 下载

# IE11提示没有找到 `lastIndexOf` 

打开 `viewer.js` 文件在第一行中加入如下代码，代码来源于：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/lastIndexOf

```js
if (typeof Uint8Array.prototype.lastIndexOf !=='function') {
    Uint8Array.prototype.lastIndexOf = function(searchElement /*, fromIndex*/) {
        'use strict';

        if (this === void 0 || this === null) {
            throw new TypeError();
        }

        var n, k,
            t = Object(this),
            len = t.length >>> 0;
        if (len === 0) {
            return -1;
        }

        n = len - 1;
        if (arguments.length > 1) {
            n = Number(arguments[1]);
            if (n != n) {
                n = 0;
            }
            else if (n != 0 && n != (1 / 0) && n != -(1 / 0)) {
                n = (n > 0 || -1) * Math.floor(Math.abs(n));
            }
        }

        for (k = n >= 0
            ? Math.min(n, len - 1)
            : len - Math.abs(n); k >= 0; k--) {
            if (k in t && t[k] === searchElement) {
                return k;
            }
        }
        return -1;
    };
}
```

# UI显示的是英文，怎么换成中文？

打开 `viewer.js` 文件，搜索 `defaultOptions.locale` 将其 `value`  改为 `zh-CN`

# 想跨域加载PDF文件怎么处理？

一、打开 `viewer.html` 文件 `<head>` 中第一行加入如下代码： 

```html
<!-- 自行下载jquery文件  -->
<script src="jquery.min.js"></script>
<script>
    var PDFData = "";
    $.ajax({
        type: "get",
        crossDomain: true,
        async: false,
        mimeType: 'text/plain;charset=x-user-defined',
        url: 'PDF文件地址',
        success: function (data) {
            PDFData = data;
        }
    });
    var rawLength = PDFData.length;
    var array = new Uint8Array(new ArrayBuffer(rawLength));
    for (var i = 0; i < rawLength; i++) {
        array[i] = PDFData.charCodeAt(i) & 0xff;
    }
    var pdf_url = array;

</script>
```

二、 打开 `viewer.js` 文件，搜索 `09.pdf`，这个文件在根目录中，自行查看文件名，然后替换成 `pdf_url`


