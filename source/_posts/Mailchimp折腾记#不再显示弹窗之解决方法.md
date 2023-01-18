---
title: Mailchimp折腾记#不再显示弹窗之解决方法
abbrlink: 5d3a37e4
date: 2020-02-25 17:19:00
categories:
tags:
---
What's past is prologue.

<!--more-->

引言

MailChimp能够设置弹窗
就是用户点开你的网站然后会出现一个弹窗
若是不小心点了取消，之后是不会再出现的：D
后来捣鼓了下。
发现这个是根据浏览器的cookie来判断是否显示的。
所以想要再次显示弹窗的话只需要`清除浏览器cookie`就可以了

给自己的blog和引导页都捣鼓了一个：D
挺好用的= =
~~虽然感觉忽悠，咳，收集不到多少邮箱233~~

### 清除cookie

然后浏览器清除cookie的话百度上有一大堆来着。
Chrome浏览器的话。
左上角`三个点`-`更多工具`-`清除浏览数据`

### 什么是cookie？


引自百度百科

> Cookie，有时也用其复数形式?[Cookies](https://baike.baidu.com/item/Cookies/187064)。类型为"小型文本文件"，是某些网站为了辨别用户身份，进行[Session](https://baike.baidu.com/item/Session/479100)跟踪而储存在用户本地终端上的数据（通常经过加密），由用户[客户端](https://baike.baidu.com/item/%E5%AE%A2%E6%88%B7%E7%AB%AF/101081)计算机暂时或永久保存的信息
> 
> Cookie 并不是它的原意"甜饼"的意思, 而是一个保存在客户机中的简单的文本文件, 这个文件与特定的?[Web]
>(https://baike.baidu.com/item/Web/150564)?文档关联在一起, 保存了该客户机访问这个Web 文档时的信息, 当客户机再次
>访问这个 Web 文档时这些信息可供该文档使用。由于"Cookie"具有可以保存在客户机上的神奇特性, 因此它可以帮助我们实现记录>用户个人信息的功能, 而这一切都不必使用复杂的[CGI](https://baike.baidu.com/item/CGI/607810)等程序?[2]??。
>
>举例来说, 一个 Web 站点可能会为每一个访问者产生一个唯一的[ID](https://baike.baidu.com/item/ID/91584), 然后以 >Cookie 文件的形式保存在每个用户的机器上。如果使用浏览器访问 Web, 会看到所有保存在硬盘上的 Cookie。在这个文件夹里
>每一个文件都是一个由"名/值"对组成的文本文件,另外还有一个文件保存有所有对应的 Web 站点的信息。在这里的每个 Cookie >文件都是一个简单而又普通的文本文件。透过文件名, 就可以看到是哪个 Web 站点在机器上放置了Cookie(当然站点信息在文件里也有保存)