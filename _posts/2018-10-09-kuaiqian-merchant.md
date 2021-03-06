---
layout: post
title: '快钱商户支付集成'
date: 2018-10-09
author: wutong
tags:  php
---

想快捷接入各种支付功能需要使用第三方支付服务，因某项目需要这种功能遂记录一下。


## 准备工作

 - 确定开发语言，本项目php
 - 与快钱签订合作协议
 - 向快钱要开发文档以便了解集成的过程（虽然文档有很多错误）
 - 向快钱要php演示代码


## 支付方式

 **网关支付**：填写支付参数跳转到快钱支付的一个地址，这个地址显示了各种支付方式
 
 **SDK支付**：在移动端（Android,iOS）中进行支付的一个功能
 
 **快捷支付**：跟支付宝的快捷支付一样，用户绑定一张银行卡进行支付
 
 
## 名词解释

 **商户私钥**：商户自己生成的私钥，用于在网关支付的时候对发送数据进行签名
 
 **商户公钥**：商户自己生成的公钥，用于在网关支付的时候快钱对商户发送的数据进行签名验证
 
 **快钱公钥**：商户登录快钱后台下载的公钥，用于在网关支付的时候对快钱发送的数据进行签名验证
 
 **快捷支付证书**：由快钱提供给商户的证书，用于在快捷支付通讯的时候传递
 
 
## 网关支付的实现
 
参照文档进行开发即可，可能会遇到如下问题
 
### 签名不正确
 
在进行签名的时候一定要按照文档提供的参数顺序进行签名计算，且如果参数为空的话不参与计算
 
### 参数值处理
 
参数值需要进行 urlencode 处理，计算出来的签名也需要进行 urlencode 处理 
 
 
## 快捷支付的实现
 
快捷支付的流程如下：

动态鉴权（相当于绑卡） -> 消费（支付） 

### 动态鉴权

传递参数并调用动态鉴权接口成功后，快钱在返回的参数用会有个token、payToken，同时会像用户的手机中发送一条验证码。
token和验证码会用于调用消费接口的时候进行传递，如果在动态鉴权接口中传递了 customerId 字段，则会保存此卡与customerId
的关联

### 消费

支付的时候需要传递银行卡号码、持卡人身份证号码、持卡人姓名、手机号、验证码、token信息，如果之前在鉴权中提供了 customerId 则
可以传递 payToken 或者 缩略卡号