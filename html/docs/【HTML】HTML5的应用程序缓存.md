# 【HTML】HTML5的应用程序缓存

## 引言

内容速递：看了本文您能了解到的知识！



## 1、什么是应用程序缓存（Application Cache）

使用 HTML5，通过创建 cache manifest 文件，可以轻松地创建 web 应用的离线版本。

## 2、应用程序缓存为应用带来三个优势

1. 离线浏览 - 用户可在应用离线时使用它们
2. 速度 - 已缓存资源加载得更快
3. 减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。

## 3、Cache Manifest

 如需启用应用程序缓存，请在文档的` <html>` 标签中包含 `manifest `属性

```
<html manifest="demo.appcache">
```

每个指定了 manifest 的页面在用户对其访问时都会被缓存。

> manifest 文件需要配置正确的 MIME-type，即 "text/cache-manifest"。

## 4、manifest 文件

manifest 文件可分为三个部分：**CACHE MANIFEST**、**NETWORK**、**FALLBACK**。

manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。

### 4.1、CACHE MANIFEST

第一行，CACHE MANIFEST，是必需的。在此标题下列出的文件将在首次下载后进行缓存。

```
CACHE MANIFEST
/theme.css
/logo.gif
/main.js
```

当 manifest 文件加载后，浏览器会从网站的根目录下载这三个文件。

然后，无论用户何时与因特网断开连接，这些资源依然是可用的。

### 4.2、NETWORK

 在此标题下列出的文件需要与服务器的连接，且不会被缓存。

```
NETWORK:
login.php
```

可以使用星号来指示所有其他资源/文件都需要因特网连接：

```
NETWORK:
*
```

### 4.3、FALLBACK

 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）。

下面的 FALLBACK 小节规定如果无法建立因特网连接，则用 "404.html" 替代 /html5/ 目录中的所有文件：

```
FALLBACK:
/html5/ /404.html
```

## 5、应用程序缓存的注释

以 "#" 开头的是注释行，但也可满足其他用途。应用的缓存会在其 manifest 文件更改时被更新。如果您编辑了一幅图片，或者修改了一个 JavaScript 函数，这些改变都不会被重新缓存。更新注释行中的日期和版本号是一种使浏览器重新缓存文件的办法。

## 6、更新缓存

一旦应用被缓存，它就会保持缓存直到发生下列情况：

- 用户清空浏览器缓存
- manifest 文件被修改（参阅下面的提示）
- 由程序来更新应用缓存

## 7、完整的 Manifest 文件

```
CACHE MANIFEST
# 2012-02-21 v1.0.0
/theme.css
/logo.gif
/main.js

NETWORK:
login.php

FALLBACK:
/html/ /offline.html
```

## 博客说明与致谢

> 文章所涉及的部分资料来自互联网整理，其中包含自己个人的总结和看法，分享的目的在于共建社区和巩固自己。
>
> 引用的资料如有侵权，请联系本人删除！
>
> 感谢万能的网络，W3C，菜鸟教程等！
>
> 感谢勤劳的[自己](https://www.guizimo.com)，[个人博客](https://blog.guizimo.com/)，[GitHub学习](https://github.com/Tangleia)，[GitHub](https://github.com/guizimo)
>
> 公众号[【归子莫】](https://welcome.guizimo.com/gzh)，小程序[【子莫说】](https://welcome.guizimo.com/zms)
>
> 如果你感觉对你有帮助的话，不妨给我点赞鼓励一下，好文记得收藏哟！关注我一起成长！
>
> 幸好我在，感谢你来！







