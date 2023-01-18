---
title: 强制https
abbrlink: 30eb72fe
date: 2020-02-27 06:39:00
---
What's past is prologue.

<!--more-->

放到`.htaccess`里就行。
逛[某幻][1]blog看到的，然后就cv过来了啧。
给自己的blog和引导页面用上了233
若用户输入的是"http://wansz.xyz",会跳转到"https://wansz.xyz"
自从Chrome68以来，对于没有ssl证书的网站就会报`不安全`了来着= =
所以这个还是挺有必要的嘛：D
然后不确定这个是否会影响Mailchimp收集rss然后推送邮件。
因为我看了看，访问“http://wansz.xyz/feed”会变成“https://wansz.xyz/feed”来着，难说



百度了下：D
引自百度百科= =
> Rewriterule是Rewrite中的一种规则。
> Rewrite,一种服务器的重写脉冲技术，它使得服务器可以支持 URL 重写，是一种最新流行的服务器技术。



1、例如我们把某个特定的 IP 直接重定向到 baidu 首页，在网站根目录的 .htaccess 文件里添加代码：
RewriteCond % 123.123.123.123 [NC]RewriteRule ^(.*)$ http://www.baidu.com/$1 [R=301] 将 123.123.123.123 这个 IP 替换成您要限制的 IP 即可
2、如果要实现多个 IP ，可以这样写：
RewriteCond % 123.123.123.123 [OR]RewriteCond % 124.124.124.124 [NC]RewriteRule ^(.*)$ http://www.baidu.com/$1 [R=301]
```

我觉得可以/好评


  [1]: https://crash-logs.ml/wrong/crash-2020-02-25_3-client.txt