---
layout:     post
title:      "关于HTTP和HTTPS的资源请求问题 "
subtitle:   "Blog中js、css加载错误"
date:       2016-08-27 2:15:00
author:     "Skylark Yan"
header-img: "img/post-bg-rwd.jpg"
catalog:    true
tags:
    - 技术问题相关
---

## 问题一开始的情况——js和css失效

我的`Blog`偶尔会出现引用的几个`js`还有`css`文件失效的情况，导致个人知乎、微博、`FaceBook`、`GitHub`的图标显示不正确，打开`Chrome`按F12进入开发者工具看到几个`css`和`js`的`Status`显示为`(blocked:mixed)`，具体如下：

![](http://upload-images.jianshu.io/upload_images/2718436-a45c91ebbb3b39fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

刚开始看到这个一脸懵逼……只能从那个`Status`为`(blocked:mixed)`下手了，然后就开始了百度……

![](https://i.imgur.com/UP39kZ1.jpg)

## 问题的原因——HTTP与HTTPS

乱七八糟到处找了找，竟然还真让我找到了问题的原因，相关的内容在[这里](https://segmentfault.com/q/1010000000648970)，大家也可以看看。

**现代浏览器都有一个默认的安全设置，`https`页面里只能请求其它`https`的资源，不能使用`http`。每个浏览器里都有开关可以取消这个限制，但是这个开关默认都是关闭的。**

而我遇到问题的原因如下：我的`Blog`没有使用自定义域名，使用的是`GitHub`提供的`username.github.io`的默认域名，而这个域名完整的`URL`应该是`https://username.github.io`，而我`Blog`中的那几个`js`和`css`的标签中的链接是这样的：

```
<link href="http://cdn.bootcss.com/font-awesome/4.6.3/css/font-awesome.min.css" rel="stylesheet" type="text/css">

<link href="http://cdn.bootcss.com/highlight.js/9.6.0/styles/github.min.css" rel="stylesheet">
```

所以我是在一个`https`页面中请求了`http`的资源，这是浏览器的默认安全设置所不允许的，自然请求失败了，那几个`js`和`css`也就失效了。由于这个`Blog`模板是出自[Hux](http://huangxuan.me/)大大的，而他使用了自定义域名，完整`URL`为：`http://huangxuan.me/`，所以在他的`Blog`中是在`http`页面请求`http`资源，自然是一切正常了。而我在使用这个模板的时候没有改动这一部分，出现这样的问题也就不奇怪了。= =

## 问题的解决方案——很简单

知道了问题的原因就好办了，我目前还要继续使用`GitHub`提供的免费域名，因为自己买的域名备案还没完成，`GitHub`的免费域名`username.github.io`强制使用`https`协议；而更改浏览器的默认安全设置也是治标不治本的方法，所以我需要把请求资源的链接也改为`https`，把上述那几个标签中的链接都改成如下就可以了：

```
<link href="https://cdn.bootcss.com/font-awesome/4.6.3/css/font-awesome.min.css" rel="stylesheet" type="text/css">

<link href="https://cdn.bootcss.com/highlight.js/9.6.0/styles/github.min.css" rel="stylesheet">
```

OK！问题解决！☺☺☺

## PS：其他收获

解决这个问题的同时，顺便更新了一下`CDN`服务，找到了一个免费的开源项目`CDN`服务器[BootCDN](http://www.bootcdn.cn/)，同时支持`http`和`https`协议，感觉蛮好用的样子，给大家安利一下。

OK，就先写到这里了，一不小心又是半夜两点多了啊= =心累……
