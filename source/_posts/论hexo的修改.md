---
title: 论hexo的修改
abbrlink: 8ffc272d
date: 2021-09-18 14:16:00
---

What's past is prologue.

<!--more-->

# 论hexo的修改

RT



# hexo首页文章只显示摘要

### 前情提要

hexo首页文章默认显示全文

因不爽

改之

### 两种方法显示摘要

##### 方法一：写概述

在文章的`front-matter`中添加`description`，其中description中的内容就会被显示在首页上，其余一律不显示。

```
---
title: 让首页显示部分内容
date: 2020-02-23 22:55:10
description: 这是显示在首页的概述，正文内容均会被隐藏。
---
```

比较不方便的是还得写一下概述，很多时候会懒得写概述，于是就需要第二种方法了。

##### 方法二：文章截断

在需要截断的地方加入：

```
<!--more-->
```

首页就会显示这条以上的所有内容，隐藏接下来的所有内容。

### 后记

来源：[https://yueyue200830.github.io/2020/02/23/%E8%AE%BE%E7%BD%AEhexo%E9%A6%96%E9%A1%B5%E5%8F%AA%E6%98%BE%E7%A4%BA%E9%83%A8%E5%88%86%E6%91%98%E8%A6%81%EF%BC%88%E4%B8%8D%E6%98%BE%E7%A4%BA%E5%85%A8%E6%96%87%EF%BC%89/](https://yueyue200830.github.io/2020/02/23/设置hexo首页只显示部分摘要（不显示全文）/)

# hexo修改站点标题等

在文件`_config.yml`中找到`#site_`

| 参数          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| `title`       | 网站标题                                                     |
| `subtitle`    | 网站副标题                                                   |
| `description` | 网站描述                                                     |
| `author`      | 您的名字                                                     |
| `language`    | 网站使用的语言                                               |
| `timezone`    | 网站时区。Hexo 默认使用您电脑的时区。[时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)。比如说：`America/New_York`, `Japan`, 和 `UTC` 。 |

# hexo增加分类

### 生成“分类”选项

在博客目录打开git，在git中输入:`hexo new page categories`

//生成“分类”页并添加tpye属性

接下来会有一个目录，找到该目录。

categories文件夹下会有个index.md文件。

添加`type: "categories"`

//注意有空格

最后文件大致如下：

```
title: categories
date: 2021-09-18 20:53:10
type: "categories"
```

保存并退出。

### 文章中添加“分类”

找到要添加分类的文章。

```
title: 论hexo的修改
categories: 七八
```

输入:`categories: 分类名`

//注意，仅限一个分类名。

# hexo部署github会重置自定义域名

//md怪不得，部署后就访问不了

//看了看自定义域名，果然它的锅

干。

解决方法：

在`source`中新建一个文件`CNAME`

//注意，无后缀

在里面添加自己的域名即可。

如我的是：

```
taoyifan.cn
www.taoyifan.cn
```

# hexo上传图片

### 修改`_config.yml`文件

```
post_asset_folder: true 
/*
默认为false，改为true
执行命令 $ hexo new post_name，在 source/_posts 中会生成文章 post_name.md 和同名文件夹 post_name。将图片资源放在 post_name 中，文章就可以使用相对路径引用图片资源了
*/
```

### 修改typora

//typora是markdown文本编辑器，不用可跳过

```
文件→偏好设置→图像
第一个选择：复制到指定路径
第二个：默认

下方五个选项，打勾前三个。
即：
对本地位置的图片应用上述规则
对网络位置的图片应用上述规则
优秀使用相对路径
```

### 使用

若使用typora，直接将图片拖到typora里即可（typora一定要经过上面配置才可），然后记得删除文件名。

若不使用，直接将图片放到同名文件夹中即可。

如：

```
![xiang](论hexo的修改/xiang.jpg)
```

直接将图片拖进来会显示这个，此时文章会显示图片

但在hexo中是不会显示图片的。

需要删除`论hexo的修改/`

即：

如果要在hexo中插入图片

假设图片名为test

则写入：

```
![](test.jpg)
```

\-

**只保留图片名**

know？

# 修改底部信息

在主题的`footer.ejs`中修改

//找不到？直接搜索，也就主题里有了。

# 一台电脑多个hexo博客搭建过程

主要参照来源:https://blog.csdn.net/qq_36759224/article/details/86546729

下面为遇到的问题

1.windows下./ssh目录

```
如我的电脑用户名为singlor
.ssh目录就在：C:\Users\singlor\.ssh
而不是，c:\users\administrator
```

2.清除本地SSH缓存，执行 ssh -add 出现报错”Could not open a connection to your authentication agent.”

```
执行如下命令　ssh-agent bash
```

3.主题下载失败，链接超时，显示”Failed to connect to github.com port 443 after 21078 ms: Timed out”

```
很玄学，多试几次就能下载成功。
```

# 上传hexo到gitee

上传时出现报错”remote: error: GE007: Your push would publish a private email address.”

解决方法：

```
设置——不公开我的邮箱地址（取消勾选）——提交邮箱设置（选择自己的邮箱）
//将邮箱设置为非私有即可
```

# 上传hexo到coding

#### **出现报错：**

```
Permission Denied (publickey)
```

#### 解决方法：

修改 `C:\Program Files\Git\etc\ssh\ssh_config` 文件，在最后添加：

```
Host *.coding.net
        HostkeyAlgorithms +ssh-rsa
        PubkeyAcceptedAlgorithms +ssh-rsa
```

而后测试 `ssh -T git@e.coding.net`即可。

# 给hexo文章加密

所用插件：https://github.com/D0n9X1n/hexo-blog-encrypt

以下内容转载至github

## 这是个啥

- ~~首先, 这是 Hexo 生态圈中 **最好的** 博客加密插件~~
- 你可能需要写一些私密的博客, 通过密码验证的方式让人不能随意浏览.
- 这在 wordpress, emlog 或是其他博客系统中都很容易实现, 然而 hexo 除外. :(
- 为了解决这个问题, 让我们有请 “hexo-blog-encrypt”.

## 特性

- 一旦你输入了正确的密码, 它将会被存储在本地浏览器的 localStorage中. 按个按钮, 密码将会被清空. 若博客中有脚本, 它将会被正确地执行.
- 支持按标签加密.
- 所有的核心功能都是由原生的 API 所提供的. 在 Node.js中, 我们使用 [Crypto](https://nodejs.org/dist/latest-v12.x/docs/api/crypto.html). 在浏览器中, 我们使用 [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API).
- [PBKDF2](https://tools.ietf.org/html/rfc2898), [SHA256](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.180-4.pdf) 被用于分发密钥, [AES256-CBC](https://csrc.nist.gov/publications/detail/sp/800-38a/final) 被用于加解密, 我们还使用 [HMAC](https://csrc.nist.gov/csrc/media/publications/fips/198/1/final/documents/fips-198-1_final.pdf) 来验证密文的来源, 并确保其未被篡改.
- 我们广泛地使用 Promise 来进行异步操作, 以此确保线程不被阻塞.
- 加密页面多主题支持, 现在已经支持的主题有 [`default`, `xray`], 更多的主题正在开发中.
- 过时的浏览器将不能正常显示, 因此, 请升级您的浏览器.

## 在线演示

- 点击 [Demo Page](https://mhexo.github.io/), **所有的密码都是 `hello`**.

## 安装

- `npm install --save hexo-blog-encrypt`
- 或 `yarn add hexo-blog-encrypt` (需要) [Yarn](https://yarnpkg.com/en/))

## 快速使用

- 将 “password” 字段添加到您文章信息头就像这样.

```
---
title: Hello World
date: 2016-03-30 21:18:02
password: hello
---
```

- 再使用 `hexo clean && hexo g && hexo s` 在本地预览加密的文章.

## 设置优先级

文章信息头 > 按标签加密

## 高级设置

### 文章信息头

```
---
title: Hello World
tags:
- 作为日记加密
date: 2016-03-30 21:12:21
password: mikemessi
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
```

### `_config.yml`

#### 示例

```
# Security
encrypt: # hexo-blog-encrypt
  abstract: 有东西被加密了, 请输入密码查看.
  message: 您好, 这里需要密码.
  tags:
  - {name: tagName, password: 密码A}
  - {name: tagName, password: 密码B}
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
```

#### 对博文禁用 Tag 加密

只需要将博文头部的 `password` 设置为 `""` 即可取消 Tag 加密.

Example:

```
---
title: Callback Test
date: 2019-12-21 11:54:07
tags:
    - A Tag should be encrypted
password: ""
---

Use a "" to diable tag encryption.
```

### 配置优先级

文章信息头 > `_config.yml` (站点根目录下的) > 默认配置

### 关于 Callback 函数

在部分博客中, 解密后部分元素可能无法正常显示或者表现, 这属于已知问题. 目前的解决办法是通过自行查阅自己的博客中的代码, 了解到在 onload 事件发生时调用了哪些函数, 并将这些函数挑选后写入到博客内容中. 如:

```
---
title: Callback Test
date: 2019-12-21 11:54:07
tags:
    - Encrypted
---

This is a blog to test Callback functions. You just need to add code at the last of your post like following:

It will be called after the blog decrypted.

<script>
    // 添加一个 script tag 与代码在文章末尾.
    alert("Hello World");
</script>
```

例子在: [Callback 例子](https://mhexo.github.io/2020/12/06/Callback-Test/).

### 对 TOC 进行加密

如果你有一篇文章使用了 TOC，你需要修改模板的部分代码。这里用 landscape 作为例子：

- 你可以在 hexo/themes/landscape/layout/_partial/article.ejs 找到 article.ejs。
- 然后找到 <% post.content %> 这段代码，通常在30行左右。
- 使用如下的代码来替代它:

```
<% if(post.toc == true){ %>
  <div id="toc-div" class="toc-article" <% if (post.encrypt == true) { %>style="display:none" <% } %>>
    <strong class="toc-title">Index</strong>
      <% if (post.encrypt == true) { %>
        <%- toc(post.origin, {list_number: true}) %>
      <% } else { %>
        <%- toc(post.content, {list_number: true}) %>
      <% } %>
  </div>
<% } %>
<%- post.content %>
```

### 禁用 Log

If you want to disable the logging, you can add a silent property in `_config.yml` and set it to true. 如果你想要禁止使用 Log, 你可以在 `_config.yml` 中增加一个 silent 属性, 并将其设置为 true.

```
# Security
encrypt: # hexo-blog-encrypt
  silent: true
```

这样就会禁止如 `INFO hexo-blog-encrypt: encrypting "{Blog Name}" based on Tag: "EncryptedTag".` 的日志.

### 加密主题

之前, 我们尝试使用 `template` 关键字来让用户能修改自己的主题. 后来发现真不是一个好主意. 所以我们现在引入了主题: `theme` 关键字.

你可以简单的使用 `theme` 在 `_config.yml` 里或者文章头, 如下:

### 文章信息头

```
---
title: Hello World
tags:
- 作为日记加密
date: 2016-03-30 21:12:21
password: mikemessi
abstract: 有东西被加密了, 请输入密码查看.
message: 您好, 这里需要密码.
theme: xray
wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
---
```

### 在 `_config.yml`

#### 示例

```
# Security
encrypt: # hexo-blog-encrypt
  abstract: 有东西被加密了, 请输入密码查看.
  message: 您好, 这里需要密码.
  tags:
  - {name: tagName, password: 密码A}
  - {name: tagName, password: 密码B}
  theme: xray
  wrong_pass_message: 抱歉, 这个密码看着不太对, 请再试试.
  wrong_hash_message: 抱歉, 这个文章不能被校验, 不过您还是能看看解密后的内容.
```

# Typecho转hexo（即将文章转换为.md格式，支持评论）

只需要数据库文件就可以。

我试过用我备份下来的数据库文件重新安装typecho，失败了。

这个软件是直接对数据库文件进行转换，无需重新搭建typecho。

地址：[www.mebyz.cn/rjdm/typechotohexo2.html](http://www.mebyz.cn/rjdm/typechotohexo2.html)

备份：

链接: https://pan.baidu.com/s/1RXP1jvbJIGX9gBs9D9VmxQ?pwd=g49m

提取码: g49m