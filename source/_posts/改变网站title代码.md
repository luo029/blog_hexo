---
title: 改变网站title代码
abbrlink: 70b2bbbe
date: 2020-04-07 03:41:00
---
What's past is prologue.

<!--more-->逛[blog][1]的时候看到的。
记录下防止啥时候自己用到但是找不到/捂脸


----------
```php
var OriginTitile = document.title;
var titleTime;
document.addEventListener('visibilitychange', function() {
   if (document.hidden) {
      document.title = '(つェ?)我藏好了哦~ ' + OriginTitile;
      clearTimeout(titleTime);
   }
else {
   document.title = '(*??｀*) 被你发现啦~ ' + OriginTitile;
      titleTime = setTimeout(function() {
      document.title = OriginTitile;
   }, 2000);
}});
```


[1]: https://www.moeloli.top/archives/moe-title.html