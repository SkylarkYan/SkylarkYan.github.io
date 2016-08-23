---
layout:     post
title:      "关于Markdown Pad 2 在win10中不显示预览的问题 "
subtitle:   "在写博文中遇到的小问题"
date:       2016-08-23 18:00:00
author:     "Skylark Yan"
header-img: "img/post-bg-js-module.jpg"
tags:
    - 技术
    - Markdown
---


> 第一次用Markdown写东西，就去找了网上都说比较好用的Markdown Pad，结果发现win10显示预览有问题，这里在找到解决方法后分享出来。


## 问题描述

在下载安装了[Markdown Pad 2](http://markdownpad.com/)之后，打开尝试用Markdown语法写了几句话，发现预览有问题，在预览窗口显示如下：

![](http://i.imgur.com/eeDfgw2.png)

同时根据它弹出的窗口提示信息跳转到了官网的[帮助信息](http://markdownpad.com/faq.html#livepreview-directx)：

![](http://i.imgur.com/6yFpd6I.png)

得，需要我装这个[Awesomium 1.6.6 SDK](http://markdownpad.com/download/awesomium_v1.6.6_sdk_win.exe) ,下载发现竟然有110M ，也是醉了。下载完安装完成后，显示预览正常，问题解决。

---

## PS:

其实这篇写完之后我已经不用Markdown Pad了，因为突然发现了最近微软新出的 [Visual Studio Code](https://code.visualstudio.com/) ,尝试了一下发现挺好用，而且支持Markdown语法并且支持预览，还有其他诸如diff等特别好用的功能，支持的语言也特别多，同时支持插件安装，并且颜值高！我感觉都想从Sublime Text 转投微软的怀抱了，打算先冷落Sublime Text 一段时间，尝试尝试 visual Studio Code ,正好用它来编辑Markdown 文件，强烈安利给大家……

