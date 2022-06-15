# 【HTML】讲讲HTML5视频播放的方式

## 引言

内容速递：看了本文您能了解到的知识！

![HTML5视频](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E8%A7%86%E9%A2%91.png)

想要网页播放视频再也不需要使用插件了，HTML本身就支持，而且更加稳定！

上节讲了HTML5的音频播放，和音频播放一样，需要借助flash才能在网页上使用视频。随着HTML5出来以后，就不需要借助flash了，本身可以通过video标签支持。

## 1、HTML5视频的播放方式

![HTML5视频的播放方式.drawio](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E8%A7%86%E9%A2%91%E7%9A%84%E6%92%AD%E6%94%BE%E6%96%B9%E5%BC%8F.drawio.png)

在 HTML 中播放视频并不容易！准确的来说是想要做好兼容并不容易！

### 1.1、embed方式

embed定义一个外部的容器，用来装放MP4等视频文件。

**例如**

```html
<embed src="movie.swf" height="200" width="200"/>
```

**缺陷**

- embed标签在 HTML 4 中是无效的，因为它是HTML5新出的标签
- 依赖浏览器的支持
- 如果浏览器不支持 Flash，那么视频将无法播放

### 1.2、obejct方式

obejct也可以定义一个外部的容器，用来装放MP4等视频文件。

**例如**

```html
<object data="movie.swf" height="200" width="200"/>
```

**缺陷**

- 依赖浏览器的支持
- 依赖插件的安装
- 如果浏览器不支持 Flash，那么视频将无法播放

### 1.3、video方式

video标签是HTML5专门为视频出的一个标签。推荐使用！

```html
<video src="horse.mp4" controls></video>
```

**效果**

![image-20220207215114260](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220207215114260.png)

**缺陷**

- video标签在 HTML 4 中是无效的，因为它是HTML5新出的标签

- 依赖浏览器的支持

## 2、最好的解决方案

上面讲了三种使用视频的方式，可以将一些结合起来使用。

**示例**

```html
<video width="320" height="240" controls="controls">
  <source src="movie.mp4" type="video/mp4" />
  <source src="movie.ogg" type="video/ogg" />
  <source src="movie.webm" type="video/webm" />
  <object data="movie.mp4" width="320" height="240">
    <embed src="movie.swf" width="320" height="240" />
  </object>
</video>
```

**讲解**

看到以上使用了 4 种不同的视频格式，这样做的好处video元素会尝试播放以 mp4、ogg 或 webm 格式中的一种来播放视频。如果均失败，则回退到 embed>元素。

**效果**

显示的效果基本与video一致！

![image-20220207215114260](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220207215114260.png)

## 3、视频格式

video 元素支持三种视频格式： MP4, WebM, 和 Ogg

| 格式 | MIME-type  |
| :--- | :--------- |
| MP4  | video/mp4  |
| WebM | video/webm |
| Ogg  | video/ogg  |

## 4、video标签

### 4.1、video的属性

一些常用的video属性，全局属性在这里就没有列出来来了。更多请到[w3school](https://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)查阅。

| 属性     | 描述                                               |
| :------- | :------------------------------------------------- |
| autoplay | 设置或返回是否在加载完成后随即播放音频/视频        |
| controls | 设置或返回音频/视频是否显示控件（比如播放/暂停等） |
| loop     | 设置或返回音频/视频是否应在结束时重新播放          |
| muted    | 设置或返回音频/视频是否静音                        |
| preload  | 设置或返回音频/视频是否应该在页面加载后进行加载    |
| src      | 设置或返回音频/视频元素的当前来源                  |

### 4.2、video的事件

事件这是我们用来跟音频发生交互的重要武器。

同样的只给出部分事件，更多请到[w3school](https://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)查阅。

| 事件       | 描述                                        |
| ---------- | ------------------------------------------- |
| pause      | 当音频/视频已暂停时                         |
| play       | 当音频/视频已开始或不再暂停时               |
| playing    | 当音频/视频在已因缓冲而暂停或停止后已就绪时 |
| canplay    | 当浏览器可以播放音频/视频时                 |
| timeupdate | 当目前的播放位置已更改时                    |

## 5、来一个视频播放器的案例

讲了那么多，不就是等一个案例吗，来！

**码上！**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1 user-scalable=0" />
    <title>video视频demo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
            font-family: "微软雅黑"
        }

        h1 {
            width: 100%;
            font-size: 1.5em;
            text-align: center;
            line-height: 3em;
            color: #33942a;
        }

        #video {
            margin: 20px 0;
            width: 100%;
            height: 200px;
        }
       
    </style>

</head>

<body>

    <h1>video视频播放demo</h1>

    <video id="video" controls src="https://www.runoob.com/try/demo_source/movie.mp4"></video>

</body>

</html>
```

**效果**

![image-20220207221322200](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220207221322200.png)

## 6、总结

视频播放的案例也走不掉的。本文主要是理论知识的讲解。

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







