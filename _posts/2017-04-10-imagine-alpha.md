---
layout: post
title: 'Yii中报Call to undefined method Imagick::setImageOpacity()'
date: 2017-04-10
author: wutong
tags:  php yii imagine
---

在使用缩略图功能的时候，报出 `Call to undefined method Imagick::setImageOpacity()` 的错误。

解决方法为修改 `setImageOpacity` 为 `setImageAlpha`