# 【HTML】HTML5的拖放你用了吗

## 引言

内容速递：看了本文您能了解到的知识！

![HTML5拖拽](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E6%8B%96%E6%8B%BD.png)

在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。

拖放的操作，多用在拖拽排序列表、游戏拼图等。

下文中出现`拖放`与`拖拽`表达同一个意思。

## 1、官方介绍

**HTML 拖放**（Drag and Drop）接口使应用程序能够在浏览器中使用拖放功能。例如，用户可使用鼠标选择可拖拽（*draggable*）元素，将元素拖拽到可放置（*droppable*）元素，并释放鼠标按钮以放置这些元素。

拖拽操作期间，会有一个可拖拽元素的半透明快照跟随着鼠标指针。

## 2、文档

可以查看拖放的一些API，包含了相关接口的说明、在应用程序中加入拖放支持的基本步骤，以及相关接口的使用简介。

文档地址：[官方文档](https://developer.mozilla.org/zh-CN/docs/Web/API/HTML_Drag_and_Drop_API)

## 3、拖拽事件

主要有八个主要的事件，完成拖拽着歌过程一系列的事件响应。

| 事件         | 事件函数      | 触发时刻                                                     |
| :----------- | :------------ | :----------------------------------------------------------- |
| `drag`       | `ondrag`      | 当拖拽元素或选中的文本时触发。                               |
| `dragend `   | `ondragend`   | 当拖拽操作结束时触发 (比如松开鼠标按键或敲“Esc”键).。        |
| `dragenter ` | `ondragenter` | 当拖拽元素或选中的文本到一个可释放目标时触发。               |
| `dragexit`   | `ondragexit`  | 当元素变得不再是拖拽操作的选中目标时触发。                   |
| `dragleave ` | `ondragleave` | 当拖拽元素或选中的文本离开一个可释放目标时触发。             |
| `dragover `  | `ondragover`  | 当元素或选中的文本被拖到一个可释放目标上时触发（每100毫秒触发一次）。 |
| `dragstart ` | `ondragstart` | 当用户开始拖拽一个元素或选中的文本时触发。                   |
| `drop `      | `ondrop`      | 当元素或选中的文本在可释放目标上被释放时触发。               |

## 4、拖拽核心

### 4.1、什么是可拖拽的？

有同学问了，上面不是说任何元素都能够拖放吗？为啥我平时拖不动？

那平时拖动了，就不叫功能了，叫BUG！

为了使元素可拖动，需要把 draggable 属性设置为 true 

```html
<div draggable="true"></div>
```

### 4.2、拖起

通过ondragstart 事件，调用dataTransfer.setData() 方法设置被拖数据的数据类型和值。

```html
<script>
  window.addEventListener('DOMContentLoaded', () => {
    const element = document.getElementById("p1");
    element.addEventListener("dragstart", (ev) => {
      ev.dataTransfer.setData("text/plain", ev.target.id);
    });
  });
</script>

<p id="p1" draggable="true">This element is draggable.</p>
```

### 4.3、拖拽数据

应用程序可以在拖拽操作中包含任意数量的数据项。每个数据项都是一个 `string`类型，典型的 MIME 类型，如：`text/html`。

```js
function dragstart_handler(ev) {
  // 添加拖拽数据
  ev.dataTransfer.setData("text/plain", ev.target.innerText);
  ev.dataTransfer.setData("text/html", ev.target.outerHTML);
  ev.dataTransfer.setData("text/uri-list", ev.target.ownerDocument.location.href);
}
```

想了解更多的xdm，可以查看 [推荐拖拽类型 (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Recommended_drag_types) 了解可拖拽的常见数据类型（如文本、HTML、链接和文件）。

### 4.4、拖拽图像

拖拽过程中，浏览器会在鼠标旁显示一张默认图片。

通过 `setDragImage()`方法自定义一张图片。

```js
function dragstart_handler(ev) {
  var img = new Image();
  img.src = 'example.gif';
  ev.dataTransfer.setDragImage(img, 10, 10);
}
```

当然如果需要图片的样式，可以使用基本的拖拽数据类型。

### 4.5、拖拽效果

在拖拽的过程中，或者鼠标停留在元素上时的反馈有 3 个效果可以定义：

1. **`copy`** 表明被拖拽的数据将从它原本的位置拷贝到目标的位置。
2. **`move`** 表明被拖拽的数据将被移动。
3. **`link`** 表明在拖拽源位置和目标位置之间将会创建一些关系表格或是连接。

通过dropEffect来设置

```js
function dragstart_handler(ev) {
  ev.dataTransfer.dropEffect = "copy";
}
```

### 4.6、放置

当拖拽一个项目到 HTML 元素中时，浏览器默认不会有任何响应。

有拖起那么必有放置，除非你犟！不松下鼠标！

这里需要借助ondrop和ondragover两个事件来完成！`dataTransfer.getData()`来设置新的数据。

```js
<script>
function dragover_handler(ev) {
 ev.preventDefault();
 ev.dataTransfer.dropEffect = "move";
}
function drop_handler(ev) {
 ev.preventDefault();
 var data = ev.dataTransfer.getData("text/plain");
 ev.target.appendChild(document.getElementById(data));
}
</script>

<p id="target" ondrop="drop_handler(event)" ondragover="dragover_handler(event)">Drop Zone</p>
```

## 5、一个拖拽案例

一个互相拖放的案例，可以从A->B，B->A。

思路：之前实现单方面的拖拽，是一个拖，一个放。那么这两者彼此都这样设置一番呢，岂不是可以实现互相的拖放？

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8"> 
<title>drag</title>
<style type="text/css">
#div1, #div2 {
	float:left; 
	width:200px; 
	height:80px; 
	margin:10px;
	border:1px solid #aaaaaa;
}
</style>
<script>
function allowDrop(ev) {
	ev.preventDefault();
}

function drag(ev) {
	ev.dataTransfer.setData("Text",ev.target.id);
}

function drop(ev) {
	ev.preventDefault();
	var data=ev.dataTransfer.getData("Text");
	ev.target.appendChild(document.getElementById(data));
}
</script>
</head>
<body>

<div id="div1" ondrop="drop(event)" ondragover="allowDrop(event)">
	<img src="https://img0.baidu.com/it/u=1047123058,3465364298&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=405" draggable="true" ondragstart="drag(event)" id="drag1" width="200" height="80">
</div>
<div id="div2" ondrop="drop(event)" ondragover="allowDrop(event)"></div>

</body>
</html>
```

**效果**

![image-20220222180034593](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220222180034593.png)

## 6、一个好用的拖拽插件

既然是学习拖拽的，那么推荐一个比较好用的Vue的拖拽组件，`vue.draggable`，它的官网地址：[Github地址](https://github.com/SortableJS/Vue.Draggable)。

![image-20220222180336664](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220222180336664.png)

里面也有其作者写的一个js公用版的。

也把中文文档地址贴一下吧，希望对你学习拖拽有帮助。[中文文档地址](https://www.itxst.com/vue-draggable/tutorial.html)。

## 7、总结

写那么多，总感觉意犹未尽！

差一个拖拽的小游戏案例？（等待安排，时间紧急，需要排期！！！）

重构前端知识体系，你要一起吗？

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







