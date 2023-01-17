---
title: An_interesting_experience_about_SSL
abbrlink: 3b3256be
date: 2020-02-25 07:52:00
categories:
tags:
---
What's past is prologue.

<!--more-->

啧
下面的不用看了
失败了啧。
卡在`No TXT Record Found. Make to set the TTL to 1 second or if you cannot set the TTL then you must wait the TTL (in seconds) so it updates before verifying the domain. Contact your DNS provider if unsure.`这里了
估摸着是我这个已经申请了ssl证书的锅
但是我感觉不太阔能
唔。
还可能是我申请的是二级域名的锅
算了就这样吧。
二级域名不捣鼓了啧。
懒得去申请了主要是：D
腾讯云那边应该是可以申请的。
本想用免费的但是申请不了┓(???`?)┏
~~明明看我组某沙同学就可以的来着(╯‵□′)╯︵┻━┻~~




### 引言
~~给你的网站来个安全套~~
咳咳
一步步截图，申请个ssl证书.jpg
也算是记录下个人折腾过程吧
~~啧作业还没写完(╯‵□′)╯︵┻━┻~~
因为喜欢，所以折腾
是么hh
咳。
然后这次我准备申请ssl证书的域名是`i.wansz.xyz`
~~输入域名的时候搜狗输入法莫名其妙给我换了个皮肤啧~~
~~不过换了的还挺好看的话说咳咳，独角兽蓝色的hh~~
~~当然现在换回来了咳咳~~
然后这个域名是图床
~~别想了私有图床hhh~~


----------
### 准备
网站：https://www.sslforfree.com/
域名：XXX


----------
### 申请
首先是打开网站，然后输入自己的域名。

完成后点击`Create Free SSL Certificate`，进入下一步。
这边一共有三个选项。
用Google翻译了下。
第一个是`自动FTP验证`-输入FTP信息自动验证域名
第二个是`手动验证`-手动上传核查文件到域名来验证域名所有权
第三个是`手动验证（DNS）`-`添加TXT记录在DNS服务器来完成验证`



我选择的是第三个
选择后然后点击`Retry Manual Verification`
之后会给你一个`TXT记录`



因为我的域名是在`阿里云`买的，所以就以阿里云为例：D
其他云的话是差不多的= =

在云控制台找到自己的域名，点击`解析`


然后选择`添加记录`
`记录类型`为`TXT`
`主机记录`为图中的①，直接复制粘贴过去即可，网站给你的那个
`记录值`为图中的②，网站给你的那个= =
`TTL`为`10分钟`

上面这些捣鼓好了之后，返回网站
然后点击`Verify _acme-challenge.XXXX`
然后因为`TTL`设置的是`十分钟`，所以需要耐心等待十分钟
如果可以设置`1秒`的话是允许设置`1秒`的
~~阿里云最少十分钟我能咋办(╯‵□′)╯︵┻━┻~~
若是出现`No TXT Record Found. Make to set the TTL to 1 second or if you cannot set the TTL then you must wait the TTL (in seconds) so it updates before verifying the domain. Contact your DNS provider if unsure.`
字样的话，慢慢等吧：D
或者调下TTL时间，最少就行。



一定要先验证一下是否解析是否生效，然后再选择下载ssl证书！切记！
~~别问我怎么知道的，得，又一个十分钟，写作业吧(╯‵□′)╯︵┻━┻~~

