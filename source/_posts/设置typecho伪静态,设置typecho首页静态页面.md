---
title: 设置typecho伪静态,设置typecho首页静态页面
date: 2020-02-24 16:08:00

---
What's past is prologue.

<!--more-->

### 设置typecho伪静态

#### 什么是伪静态？
> 伪静态是相对真实静态来讲的，通常我们为了增强搜索引擎的友好面，都将文章内容生成静态页面，但是有的朋友为了实时的显示一些信息。或者还想运用动态脚本解决一些问题。不能用静态的方式来展示网站内容。但是这就损失了对搜索引擎的友好面。怎么样在两者之间找个中间方法呢，这就产生了伪静态技术。伪静态技术是指展示出来的是以html一类的静态页面形式，但其实是用ASP一类的动态脚本来处理的。

简单来说
以域名`wansz.xyz`为例
如果用这个域名搭建博客的话
点击一篇文章
域名应该是`wansz.xyz/index.php/325`
而设置了`伪静态`
点击一篇文章
域名应该是`wansz.xyz/325.html`
影响，唔，不大
但是缩短了一点，很简介，且有些人不是会看`index.php`不顺眼的嘛owo

#### 如何设置？
参照了下这篇文章：https://blog.csdn.net/yiferhuang/article/details/86473209

首先在你的`程序根目录`创建一个`文件`
文件名为`.htaccess`
（有`.`不要忘记了，以及没有后缀，就是这么一个名字
（话说`.htaccess`就是后缀来着#run
（如果不知道`程序根目录`在哪里的话，唔，你看看你程序的`index.php`在哪里，`.htaccess`文件就放在哪里

然后在`.htaccess`文件中放入以下代码
```
<IfModule mod_rewrite.c>
RewriteEngine On
# 下面是在根目录，文件夹要修改路径
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ /index.php/$1 [L]
</IfModule>
```
直接cv过去就好，不需要修改什么

（针对`Apache`服务器而言是这样子的
（其他的话，我没有搞懂，因为我已经配置成功了就没去看其他例子
（我直接cv下好了，防止丢失

Linux Apache环境（Nginx）
```
location / {
index index.html index.php;
if (-f $request_filename/index.html) {
rewrite (.*) $1/index.html break;
}
if (-f $request_filename/index.php) {
rewrite (.*) $1/index.php;
}
if (!-f $request_filename) {
rewrite (.*) /index.php;
}
}
```

Windows IIS伪静态(httpd.ini)
```
[ISAPI_Rewrite]
# 3600 = 1 hour
CacheClockRate 3600
RepeatLimit 32
# 中文tag解决
RewriteRule /tag/(.*) /index\.php\?tag=$1
# sitemapxml
RewriteRule /sitemap.xml /sitemap.xml [L]
RewriteRule /favicon.ico /favicon.ico [L]
# 内容页
RewriteRule /(.*).html /index.php/$1.html [L]
# 评论
RewriteRule /(.*)/comment /index.php/$1/comment [L]
# 分类页
RewriteRule /category/(.*) /index.php/category/$1 [L]
# 分页
RewriteRule /page/(.*) /index.php/page/$1 [L]
# 搜索页
RewriteRule /search/(.*) /index.php/search/$1 [L]
# feed
RewriteRule /feed/(.*) /index.php/feed/$1 [L]
# 日期归档
RewriteRule /2(.*) /index.php/2$1 [L]
# 上传图片等
RewriteRule /action(.*) /index.php/action$1 [L]
```

#### 配置完后如何在typecho后台设置？

 - 进入`后台`
 - `设置`-`永久链接`
 - `是否使用地址重写功能`选择`启用`，`自定义文章路径`选择`除第一个（默认风格）之外的任意一个`
 - 保存设置

（可能会提示`失败，是否要强制设置`什么的，不用管，选择`强制设置`就行了
（大概就这么个意思，忘了：D


----------

### 设置typecho首页静态页面

来源：https://itlu.org/articles/1857.html

#### 新建文件
新建文件`f5.php`
放在`软件根目录`（即`index.php`所在的目录

#### 放入代码
将下列代码放入`f5.php`中

```php
<?php
$nowtime=time();
$pastsec = $nowtime - $_GET["t"];
if($pastsec<600)
{
exit; //10分钟更新一次，时间可以自己调整
}
ob_start(); //打开缓冲区
include("index.php");
$content = ob_get_contents(); //得到缓冲区的内容
$content .= "\n<script language=javascript src=\"f5.php?t=".$nowtime."\"></script>"; //加上调用更新程序的代码

file_put_contents("index.html",$content);
if (!function_exists("file_put_contents"))
{
function file_put_contents($fn,$fs)
{
$fp=fopen($fn,"w+");
fputs($fp,$fs);
fclose($fp);  
}
}
?>
```

#### 设置
放入代码之后，在浏览器中打开`域名/f5.php`
如我的网站是`wansz.xyz`，那么我应该打开的是`wansz.xyz/f5.php`
打开后你看到的依旧是`首页`，且将会有一个`index.heml`文件在软件根目录生成。
`刷新`，`重新进入`网站（不用进入`域名/f5.php`）
`右键`页面，`查看网页源代码`/`审查元素`都可以
若是末尾有出现
`<script language=javascript ……"></script>`
即成功
即说明你访问的是“index.html”页面

#### 补充

若是`index.html`生成成功，末尾却没有出现
`<script language=javascript ……"></script>`
可能是程序默认访问`index.php`的权限比`index.html`高。

`宝塔`的话在`站点修改`中的`默认文档`中
将`index.html`放在`index.php`上面即可

`cPanel`的话在`.heaccess`中添加代码`DirectoryIndex index.html index.php index.htm`然后保存即可。
（可以放在文档最上面，任意位置。

#### 后话
唔。
设置typecho首页静态页面那个
刚刚发现你发布文章的话是不能第一时间显示的
原因是这个：
```php
if($pastsec<600)
{
exit; //10分钟更新一次，时间可以自己调整
}
```

代码里的时间是，你想要刷新的时间（分钟）*60=填写的时间
（填写的是`秒`计的：D
我觉得太慢了就设置了一分钟刷新一次，然后代码是这样子的：
```php
if($pastsec<60)
{
exit; //1分钟更新一次，时间可以自己调整
}
```

（修改了后没有改的话可以试试重新生成下`index.html`文件


----------
![](https://buyao.mobi/i/2020/02/25/nfrtz3.png)
~~(小媳妇受欺负语气哈哈哈哈哈哈哈哈哈哈哈~~
应某沙强烈要求，补上图片hhhh
感谢我方[幻沙][1]同学。
也是，他最先提出来，然后我问他是不是捣鼓了伪静态= =
然后他说是，然后我就向他取了下~~精~~，经
也的确在我捣鼓的时候给我了一些帮助
行吧：D
(╯‵□′)╯︵┻━┻
咳，嘘。

[1]: http://crash-logs.ml/