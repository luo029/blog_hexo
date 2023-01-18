---
title: typecho加上gzip压缩，使网站更快加载
abbrlink: d5cfd609
date: 2020-04-19 15:40:00
categories:
tags:
---
What's past is prologue.

<!--more-->

放到网站`根目录`的`index.php`文件中即可，建议放在开头。（不是`主题`的那个`index.php`，是整个`主程序`的）
代码：

```php
/*添加Gzip*/
ob_start('ob_gzhandler');
```

可以去<http://tool.chinaz.com/gzips/>查看是否开启。
gzip是一项压缩技术，减小网络传输的数据量，使网站得到更快的加载。
~~各位可以自行尝试~~
~~反正我加了后不管是不是心理作用，总之是变快了挺多。。。三分之一有余吧？~~
