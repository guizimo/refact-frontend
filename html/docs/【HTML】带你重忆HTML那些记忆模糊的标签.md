# 【HTML】带你重忆HTML那些记忆模糊的标签

## 引言

github：[【HTML】带你重忆HTML那些记忆模糊的标签](https://github.com/guizimo/refact-frontend/blob/main/html/docs/%E3%80%90HTML%E3%80%91%E5%B8%A6%E4%BD%A0%E9%87%8D%E5%BF%86HTML%E9%82%A3%E4%BA%9B%E8%AE%B0%E5%BF%86%E6%A8%A1%E7%B3%8A%E7%9A%84%E6%A0%87%E7%AD%BE.md)

内容速递：看了本文您能了解到的知识！

![HTML标签](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML%E6%A0%87%E7%AD%BE.png)

上节，说了HTML是标记语言，那么最重要的就是标记，也就是标签。

那标签那么多？要在这里全部写出来？

当然否。这里会讲解常用的标签。（常用达到70%）

希望在各种前端框架频出的年代，HTML依然牢记于心。

## 1、回顾

在刚开始介绍HTML的时候，讲了一个简单的demo，这里贴出来。

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>我是一个标题</title>
</head>
<body>
	<h1>我是一个页面内容的标题</h1>
	<div>我是一个美男子，你信吗？</div>
</body>
</html>
```

## 2、HTML元素

### 2.1、什么是HTML元素？

HTML 元素指的是从`开始标签（start tag）`到`结束标签（end tag）`的所有代码。

具体什么意思呢

```html
<div>我是一个美男子，你信吗？</div>
```

像上述代码就是一个div元素，它包含了div开始标签，div元素内容，div结束标签，它们一起组合成为了一个div元素。

```html
<body>
	<h1>我是一个页面内容的标题</h1>
	<div>我是一个美男子，你信吗？</div>
</body>
```

同样的以上的代码描述了一个body元素。

### 2.2、空HTML元素

在之后的标签学习中，有那么一个标签`<br>`， 这个标签定义换行。像这种HTML 元素被称为空元素，它是在开始标签中关闭的。

但！为了以后版本迭代和规划，在 XHTML、XML 以及未来版本的 HTML 中，所有元素都必须被关闭。

> 未来的 HTML 版本不允许省略结束标签！

## 3、HTML标签

![HTML标签类型](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML%E6%A0%87%E7%AD%BE%E7%B1%BB%E5%9E%8B.png)

这里按照功能分类讲解

### 3.1、基础标签

**列表：**

- `<!DOCTYPE>`  定义文档类型。
- `<html>` 定义 HTML 文档。
- `<head>`定义关于文档的信息。
- `<title>`定义文档的标题。
- `<body>`定义文档的主体。
- `<br>`定义换行。
- `<h1> - <h6>`定义 HTML 标题。
- `<p>`定义段落。
- `<!-- -->`定义注释。

**示例**：

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>我是一个标题</title>
</head>
<body>
	<h1>我是一个页面内容的标题h1</h1>
	<p>我是一个一个段落<br>我是一个一个段落<br>我是一个一个段落<br>我是一个一个段落<br>我是一个一个段落</p>
  <!-- <p>我是一段隐藏的段落</p> -->
</body>
</html>
```

**效果**：

![image-20220118151800653](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118151800653.png)

看起来，学会了这些基础标签，就可以在网上发一篇小作文啦。实现文字自由？

单独的文本未免太过于单调，来点修饰

### 3.2、修饰文本（格式化）

**列表：**

- `<abbr>`  定义文档类型。最初是在 HTML 4.0 中引入的，表示它所包含的文本是一个更长的单词或短语的缩写形式。

```html
<abbr title="ni shi zui hao de">nszhd</abbr>
```

![image-20220118155417168](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118155417168.png)

- `<i>` 显示斜体文本效果。
- `<b>`呈现粗体文本效果。
- `<em>`定义强调文本。
- `<strong>`把文本定义为语气更强的强调的内容
- `<u>`定义下划线文本。

**示例：**

```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>我是一个标题</title>
</head>
<body>
		<p><i>我是一个i段落</i></p>
    <p><u>我是一个u段落</u></p>
    <p><em>我是一个em段落</em></p>
    <p><strong>我是一个strong段落</strong></p>
    <p><b>我是一个b段落</b></p>
</body>
</html>
```

**效果：**

![image-20220118160731574](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118160731574.png)

### 3.3、表单

**列表：**

- `<form>` 定义供用户输入的 HTML 表单。
- `<input>` 定义输入控件。
- `<textarea>` 定义多行的文本输入控件。
- `<button>`定义按钮。
- `<select>`定义选择列表（下拉列表）。
- `<option>`定义选择列表中的选项。

**示例：**

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>我是一个标题</title>
</head>

<body>
  
  
    <form action="form_action.asp" method="get">
        <p>name: <input type="text" name="name" /></p>
        <p>password: <input type="password" name="password" /></p>
        <p><textarea>请填写简介</textarea></p>
        <p>select：
            <select>
                <option value="wo">我</option>
                <option value="zui">最</option>
                <option value="shuai">帅</option>
            </select>
        </p>
        <input type="submit" value="Submit" />
    </form>


</body>

</html>
```

**效果：**

![image-20220118162520792](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118162520792.png)

### 3.4、图像、音频与视频

**列表：**

- `<img>`  定义图像。
- `<canvas>` 定义图形。
- `<svg>`定义 SVG 图形的容器。
- `<audio>`定义声音内容。
- `<video>`定义视频。
- `<source>`定义媒介源。

**示例：**

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>我是一个标题</title>
</head>

<body>

    <p>
        img: <img src="https://lf-cdn-tos.bytescm.com/obj/static/xitu_extension/static/baidu.9627e61f.png" />
    </p>
    <p>
        canvas: <canvas id="myCanvas"></canvas>
    </p>
    <p>
        svg: <svg width="100" height="100">
            <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
        </svg>
    </p>
    <p>audio: 
        <audio src="http://96.ierge.cn/15/235/471737.mp3" controls="controls"></audio>
    </p>
    <p> video: 
        <video src="https://vd3.bdstatic.com/mda-kiq250jsxvmh23gu/hd/cae_h264_nowatermark/mda-kiq250jsxvmh23gu.mp4"></video>
    </p>


</body>

<script type="text/javascript">
    var canvas = document.getElementById('myCanvas');
    var ctx = canvas.getContext('2d');
    ctx.fillStyle = '#FF0000';
    ctx.fillRect(0, 0, 80, 100);
</script>

</html>
```

**效果**：

![image-20220118164420834](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118164420834.png)

### 3.5、链接

**列表**：

- `<a>`  定义锚。

```html
<a href="https://www.baidu.com">我是百度</a>
```

- `<link>` 定义文档与外部资源的关系。

```html
<link rel="stylesheet" type="text/css" href="demo.css" />
```

### 3.6、列表类型

**列表**：

- `<ul>`  定义无序列表。
- `<ol>` 定义有序列表。
- `<li>`定义列表的项目。
- `<dl>`定义定义列表。
- `<dd>`定义定义列表中项目的描述。
- `<dl>`定义定义列表中的项目。

**示例**：

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>我是一个标题</title>
</head>

<body>

    <ul>
        <li>我是第一</li>
        <li>我是第二</li>
        <li>我是第三</li>
    </ul>

    <ol>
        <li>我是第一</li>
        <li>我是第二</li>
        <li>我是第三</li>
    </ol>

    <dl>
        <dt>我</dt>
        <dd>很帅</dd>
        <dt>你</dt>
        <dd>帅吗</dd>
    </dl>


</body>

</html>
```

**效果**：

![image-20220118170046796](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118170046796.png)



### 3.7、表格

**列表**：

- `<table>`  定义表格
- `<caption>` 定义表格标题。
- `<th>`定义表格中的表头单元格。
- `<tr>`定义表格中的行。
- `<td>`定义表格中的单元。
- `<thead>`定义表格中的表头内容。
- `<tbody>`定义表格中的主体内容。
- `<tfoot>`定义表格中的表注内容（脚注）。

**示例**：

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>我是一个标题</title>
</head>

<body>

    <table border="1">
        <thead>
            <tr>
                <th>姓名</th>
                </th>
                <th>分数</th>
            </tr>
        </thead>

        <tfoot>
            <tr>
                <td>小明</td>
                <td>100</td>
            </tr>
        </tfoot>

        <tbody>
            <tr>
                <td>小红</td>
                <td>70</td>
            </tr>
            <tr>
                <td>小东</td>
                <td>80</td>
            </tr>
        </tbody>
    </table>


</body>

</html>
```

**效果**：

![image-20220118172018318](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220118172018318.png)



### 3.8、其他

**列表**：

- `<script>`  定义客户端脚本。

```html
<script type="text/javascript">
document.write("Hello World!")
</script>
```

- `<object>` 定义嵌入的对象。
- `<embed>`为外部应用程序（非 HTML）定义容器。

```html
<embed src="test.png" />
```

- `<head>`定义关于文档的信息。
- `<meta>`定义关于 HTML 文档的元信息。
- `<base>`定义页面中所有链接的默认地址或默认目标。

## 4、总结

HTML的标签很多，相信大多数的xdm都了解。但并非都能记得。

告诉你们一件事，我在做HTML的面试题集，准确率竟然只有60%多。这也是我写本篇文章的目的。查漏补缺。

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







