# 【HTML】深入WebSocket的世界

















## 1、什么是WebSocket

`WebSocket` 是 HTML5 开始提供的一种在单个 TCP 连接上进行**全双工通讯**的协议。

说到`WebSocket`那就离不开它的好兄弟`HTTP`，它们都位于OSI模型的应用层，并且都依赖于传输层的`TCP`协议。但是，说到这里并不足以说明它们之间的关系，不是吗？

在**RFC 6455**中找到：

> it is designed to work over HTTP ports 80 and 443 as well as to support HTTP proxies and intermediaries.
>
> WebSocket通过HTTP端口80和443进行工作，并支持HTTP代理和中介。













