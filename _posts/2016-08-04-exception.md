---
layout: post
title: 错误记录
date: 2016-06-28
categories: 
tags: [记录]
description: 错误记录
---

####运行项目时报错unable to instantiate application,Didn't find class "xxx.xxx.xxx" on path: DexPathList
> 项目运行背景,一直是可以正常运行的,但是手机升级到6.0(5.0)之后,同时使用了新版本的Android Studio 并且SDK 24 .在运行时一直报无法找到application类,但是代码并没有更改.
> 猜想到应该是ART预编译项目后,application没有找到类的加载器,所以一直处于无法找到类的状况.随后将应用卸载,重新安装问题解决.

- 记录在此, 待空闲时仔细研究一下这个问题.