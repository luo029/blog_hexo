---
title: '捣鼓了下sitemap,发现个免费申请ssl网站'
abbrlink: 5df18c6a
date: 2020-02-25 04:43:00
---
What's past is prologue.

<!--more-->### 捣鼓了下sitemap

sitemap我是配合百度站长平台来使用的
用处是`自动向百度提交网站更新文章`
（不过反正我是发现百度没有收录我这个blog就是了hhhhh

#### 下载插件
插件：[HPSitemap][1]
下载完后上传至`plugins`文件里面
解压后记得`重命名`，不要带有`-（破折号）`即可
（一般我是直接重命名为`HPSitemap`）

#### 配置插件
进入~~gayecho~~，咳，`typecho`后台，`控制台`-`插件`-启用`HPSitemap`
（如果现实`sever error`,可能是名字问题，重命名下= =
然后点击`HPSitemap`-`设置`
`设置生成sitemap的目录(根目录即站点根目录)`：`sitemap`
（默认即可
`设置接口密匙`：`数字，随便写`
（比如我设置的接口密匙是`123`，那么在`设置接口密匙`这里我就填写`123`
`是否使用百度移动协议`：`随意`
（我选择的是`否`

#### 尝试运行
浏览器地址栏里输入`你的网站/action/update_sitemap?auth=接口密匙`
如我的接口密匙填写的`123`,网站是`wansz.xyz`
那么我输入的就是`wansz.xyz/action/update_sitemap?auth=123`
如果`未设置伪静态`
那么浏览器地址栏输入`你的网站/index.php/action/update_sitemap?auth=接口密匙`
（如何确认自己是否是`伪静态`？
（随便点击一篇自己blog的文字，如果地址栏那边有出现`index.php`字样则`未设置伪静态`
（设置伪静态可以参考我写的[文章][2]（可点击），设置typecho伪静态的：D


----------
打开网址`你的网站/index.php/action/update_sitemap?auth=接口密匙`后
应该会显示以下内容：
```
Done for categories index.
Done for pages index.
Done for posts index.
Generating sitemap index for file 1
Done for remaining index.
Done for sitemap generating, result sitemap file is XXXXXXXXX
```
（若显示了则说明前面步骤都是对了的= =
到此，差不多就完成了。
唔。
插件会生成一个`sitemap`文件夹，里面有两个文件，分别为`sitemap.xml`和'sitemap_1.xml'
`sitemap`文件夹会生成在`程序根目录`，即`index.php`所在的目录
可以自行访问下：D
比如域名是`wansz.xyz`
访问的话应该就是`wansz.xyz/sitemap/sitemap.xml`
也可以是`wansz.xyz/sitemap/sitemap_1.xml`
自此，没了。

#### 后话
`sitemap`捣鼓好了后可以在[百度站长平台][3]提交
首先是注册，然后填写自己的网站域名
然后是分别点击`网站支持`-`链接提交`



然后往下滑，选择`自动提交`，然后选择`sitemap`



提交网址就好，格式是`网站/sitemap/sitemap_1.xml`
（我觉得是这个，当然你是可以两个都提交的，就是`sitemap.xml`和`sitemap_1.xml`
（个人两个都提交了；D

然后在逛知乎的时候看到[一篇文章][4]，用户Vincent的回答让我有些许感触：D

> 我觉得做站本身就是，坚持做好原创内容，坚持每天写些东西。等你回到头的时候，百度已经很喜欢你了。关注一个非自己能控制的东西是很累的。

嗯，不错：D
~~至少我那不被百度收录的无奈心态稍有平复了来着hhh~~
~~话说莫名其妙被搜狗收录了一个首页，虽然最先出现的是我的网盘啧，但是网盘我设置了重定向，跳转到我的个人引导页来着233~~


----------


### 发现个免费申请ssl网站
凑字数的。
哈哈哈哈哈
咳。
https://www.sslforfree.com/
不确定是否能用，但是估摸着能用：D
我这边因为不需要所以就没有捣鼓了233
从一位博主的blog上看来的：D
https://catni.cn/archives/220/
各位可以去看看：D
大致配置ssl证书的流程就几样。
域名解析设置，证书配置。
（我目前用的是百度云和腾讯云的。
（阿里云的申请了，也没去看通过没通过，反正他审核通过还是不通过我都懒得用了(o?ω`o)?


----------
没了。
听课。
上课了。
据说要考试。
从心了。
溜了。

[1]: https://github.com/invelop/Typecho-HPSitemap
[3]: https://ziyuan.baidu.com/
[4]: https://www.zhihu.com/question/58560210/answer/715508954