# 【HTML】不来看看HTML5的WebStorage吗

面试官：讲讲sessionStorage和localStorage的区别？

回答：en～，一个有限制，一个无？

技术选型：做一个离线数据的缓存！

回答：好像都能实现，随便用？

## 引言

内容速递：看了本文您能了解到的知识！

![WebStorage](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/WebStorage.png)

## 1、什么是 HTML5 Web 存储

它是一种可以在本地存储用户的浏览数据的一种技术。

主要的目的是克服由cookie所带来的一些限制，当数据需要被严格控制在客户端时，不需要持续的将数据发回给到服务器，那么这时就会使用WebStorage。

## 2、WebStorage两个主要目标

提供一种在cookie之外存储会话数据的路径。

提供一种存储大量可以跨会话存在的数据的机制。

## 3、Web Storage

![WebStorage.drawio](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/WebStorage.drawio.png)

HTML5提供了两个客户端存储数据的两个对象：

- `sessionStorage` 为每一个给定的源（given origin）维持一个独立的存储区域，该存储区域在页面会话期间可用（即只要浏览器处于打开状态，包括页面重新加载和恢复）。
- `localStorage` 同样的功能，但是在浏览器关闭，然后重新打开后数据仍然存在。

## 4、sessionStorage

用于临时保存同一窗口(或标签页)的数据，在关闭窗口或标签页之后将会删除这些数据。

### 4.1、特性

- 页面会话在浏览器打开期间一直保持，并且重新加载或恢复页面仍会保持原来的页面会话。
- **在新标签或窗口打开一个页面时会复制顶级浏览会话的上下文作为新会话的上下文，**这点和 session cookies 的运行方式不同。
- 打开多个相同的 URL 的 Tabs 页面，会创建各自的 `sessionStorage`。
- 关闭对应浏览器标签或窗口，会清除对应的 `sessionStorage`。 

>  `http://example.com` 与 `https://example.com` 的 sessionStorage 相互隔离

### 4.2、API

- 保存数据：sessionStorage.setItem(key,value);
- 读取数据：sessionStorage.getItem(key);
- 删除单个数据：sessionStorage.removeItem(key);
- 删除所有数据：sessionStorage.clear();
- 得到某个索引的key：sessionStorage.key(index);

## 5、localStorage

用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去除。

### 5.1、特性

- 存储的数据不会随着用户浏览时会话过期而过期，但会应用户的请求而删除
- 浏览器也因为存储空间的限制或安全原因而删除
- 存储的数据可以同一个浏览器的**多个窗口共享**

> 只能存储字符串，如果是`json`对象的话，可以将对象`JSON.stringify() `编码后存储

### 5.2、API

- 保存数据：localStorage.setItem(key,value);
- 读取数据：localStorage.getItem(key);
- 删除单个数据：localStorage.removeItem(key);
- 删除所有数据：localStorage.clear();
- 得到某个索引的key：localStorage.key(index);

## 6、sessionStorage与localStorage的差异

**1、生命周期**

**localStorage**的生命周期是永久的，关闭页面或浏览器之后localStorage中的数据也不会消失。localStorage除非主动删除数据，否则数据永远不会消失。

**sessionStorage**的生命周期是在仅在当前会话下有效。sessionStorage引入了一个“浏览器窗口”的概念，sessionStorage是在同源的窗口中始终存在的数据。只要这个浏览器窗口没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在。但是sessionStorage在关闭了浏览器窗口后就会被销毁。**同时独立的打开同一个窗口同一个页面，sessionStorage也是不一样的。**

**2、存储大小**

localStorage和sessionStorage的存储数据大小一般都是：5MB。

**3、存储位置**

localStorage和sessionStorage都保存在客户端，不与服务器进行交互通信。

**4、存储内容类型**

localStorage和sessionStorage只能存储字符串类型，对于复杂的对象可以使用ECMAScript提供的JSON对象的stringify和parse来处理。

## 7、WebStorage的优点

> 注意：这里是WebStorage同cookie相比。

![WebStorage的优点.drawio](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/WebStorage%E7%9A%84%E4%BC%98%E7%82%B9.drawio.png)

**1、存储空间更大**

cookie为4KB，而WebStorage是5MB。

**2、节省网络流量**

WebStorage不会传送到服务器，存储在本地的数据可以直接获取，也不会像cookie一样每次请求都会传送到服务器，所以减少了客户端和服务器端的交互，节省了网络流量。

**3、便捷性**

对于那种只需要在用户浏览一组页面期间保存而关闭浏览器后就可以丢弃的数据，sessionStorage会非常方便；

**4、安全性**

WebStorage不会随着HTTP header发送到服务器端，所以安全性相对于cookie来说比较高一些，不会担心截获，但是仍然存在伪造问题；

## 8、总结

sessionStorage和localStorage的使用越来越多了，也慢慢成为一种必备的前端知识了。更多详细的用法还是需要在日常工作中去提炼和加深印象，本文最大的作用还是温故知识，查漏补缺！

既然看到了这里，我正在重构前端知识体系，你要一起吗？

## 系列文章



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







