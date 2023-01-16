---
title: 修改了下版权说明,cv后有版权显示,字数统计,目录树插件,显示标签
date: 2020-02-16 11:30:00

---
What's past is prologue.

<!--more-->### 版权说明
修改了下版权说明。
最终结果：

```
<!--版权说明-->
<blockquote class="content-copyright" style="margin-top:50px;background-color:rgba(255,255,255,0.7);border-left:5px solid #dde6e9!important;">
    <p>
        <font color="RosyBrown ">
            <b>
                版权声明
            </b>
            ：若文中无特殊说明，则本文为原创文章，版权归
            <a href="https://wansz.xyz" target="_blank">
                辛落
            </a>
            所有。
        </font>
    </p>
        <font color="RosyBrown ">
       <strong>本文链接：</strong><a target="_blank" href="<?php $this->permalink() ?>"><?php $this->permalink() ?></a>
        </font>
    <p>
        <font color="RosyBrown ">
            所有原创文章采用
            <a href="https://creativecommons.org/licenses/by-nc/4.0/deed.zh" target="_blank">
                知识共享署名-非商业性使用 4.0 国际许可协议
            </a>
            进行许可。
            <br>
        </font>
              </p>
            <p>
        <font color="RosyBrown">
            您可以自由的转载和修改，但请务必注明文章来源并且不可用于商业目的。
        </font>
    </p>
            <p>
        <font color="Peru ">
            <?php echo art_count($this->cid); ?>
        </font>
    </p>


</blockquote>
```

主要是修改了下颜色，以及添加了字数统计


----------


### 版权显示
就是当用户复制我的博文后，粘贴出来后会有显示出处之类。
例子：
```
著作权归作者所有。
商业转载请联系作者获得授权，非商业转载请注明出处。
作者：辛落
链接：https://wansz.xyz/index.php/archives/236/
来源：https://wansz.xyz/

四比较忌讳= =
233
嗯。
```

代码：
```
  <script>
document.body.addEventListener('copy', function (e) {
    if (window.getSelection().toString() && window.getSelection().toString().length > 10) {
        setClipboardText(e);
    }
}); 
function setClipboardText(event) {
    var clipboardData = event.clipboardData || window.clipboardData;
    if (clipboardData) {
        event.preventDefault();
        var htmlData = ''
            + '著作权归作者所有。<br>'
            + '商业转载请联系作者获得授权，非商业转载请注明出处。<br>'
            + '作者：<?php $this->author() ?><br>'
            + '链接：' + window.location.href + '<br>'
            + '来源：<?php $this->options->siteUrl(); ?><br><br>'
            + window.getSelection().toString();
        var textData = ''
            + '著作权归作者所有。\n'
            + '商业转载请联系作者获得授权，非商业转载请注明出处。\n'
            + '作者：<?php $this->author() ?>\n'
            + '链接：' + window.location.href + '\n'
            + '来源：<?php $this->options->siteUrl(); ?>\n\n'
            + window.getSelection().toString();
        clipboardData.setData('text/html', htmlData);
        clipboardData.setData('text/plain',textData);
    }
}
</script> 
```

我是有稍微修改过得。
我将`+ '作者：<?php $this->author() ?>\n'`改成了`+ '作者：辛落\n'`
以及`+ '作者：<?php $this->author() ?><br>'`改成了`+ '作者：辛落<br>'`
因为这个获取的是你的用户名，所以实际会显示“Supine”，然后我觉得不太好，就手动改了，毕竟是个人blog。
从一篇[博文][1]上看到的

----------


###字数统计
从一篇[博文][2]上看到的

首先，将下列代码放到function.php处。
（有些主题可能没有这个文件，可以自行创建一个，或者从其他主题处cv一个过来，若是创建后无法使用的话
```
function art_count ($cid){
$db=Typecho_Db::get ();
$rs=$db->fetchRow ($db->select ('table.contents.text')->from ('table.contents')->where ('table.contents.cid=?',$cid)->order ('table.contents.cid',Typecho_Db::SORT_ASC)->limit (1));
$text = preg_replace("/[^\x{4e00}-\x{9fa5}]/u", "", $rs['text']);
echo '共'.mb_strlen($text,'UTF-8').'字';
}
```

然后只需要在需要字数统计的地方加上`<?php echo art_count($this->cid); ?>`即可
我是直接放到版权说明这里了：D
不需要手动添加233


----------


###目录树插件

嗯，安装了一个[目录树][3]插件。
能够设置在"未使用标题h1，h2时是否隐藏"
以及"是否引用jQuery"


----------


###显示标签
在`post.php`中加入`<br>Tag:<?php $this->tags(); ?>`
然后标签就可以正常显示了_(:з」∠)_
顺便可以在归档页面里加入标签了_(:з」∠)_

[1]: https://www.pandasoda.cn/archives/copyright-of-articles.html
[2]: https://www.eyuyun.com/196.html
[3]: https://github.com/hongweipeng/MenuTree