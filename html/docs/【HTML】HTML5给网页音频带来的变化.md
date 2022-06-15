# 【HTML】HTML5给网页音频带来的变化

## 引言

内容速递：看了本文您能了解到的知识！

![HTML5音频](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E9%9F%B3%E9%A2%91.png)

音乐播放，相信大家都很熟悉，但是早在之前的音乐播放之前，你的浏览器会问你，是否下载flash插件。然而现在，估计一些年轻的开发者都不用了解flash是啥了。因为HTML5来了，它改变了这一切。

## 1、HTML5音频的播放方式

![HTML5音频的播放方式.drawio](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E9%9F%B3%E9%A2%91%E7%9A%84%E6%92%AD%E6%94%BE%E6%96%B9%E5%BC%8F.drawio.png)

是的，HTML5带来了不止一种能够播放音频的方式。

### 使用插件

浏览器插件是一种扩展浏览器标准功能的小型计算机程序。

插件可以使用 **object** 标签 或者 **embed** 标签添加在页面上。

### embed方式

embed定义一个外部的容器，用来装放MP3等音频文件。

**例如**

```html
<embed height="50" width="100" src="demo.mp3">
```

**效果**

![image-20220120231414621](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220120231414621.png)

**缺陷**

- embed标签在 HTML 4 中是无效的，因为它是HTML5新出的标签
- 依赖浏览器的支持
- 依赖插件的安装

### obejct方式

obejct也可以定义一个外部的容器，用来装放MP3等音频文件。

**例如**

```html
<object height="50" width="100" src="demo.mp3"></object>
```

**效果**

![image-20220120231414621](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220120231414621.png)

**缺陷**

- 依赖浏览器的支持
- 依赖插件的安装

### audio方式

audio标签是HTML5专门为音频出的一个标签。推荐使用！

```html
<audio src="horse.mp3" controls></audio>
```

**效果**

![image-20220120231347590](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220120231347590.png)

**缺陷**

- embed标签在 HTML 4 中是无效的，因为它是HTML5新出的标签

- 依赖浏览器的支持

## 2、最好的解决方案

上面讲了三种使用音频的方式，可以将一些结合起来使用。

**示例**

```html
<audio controls height="100" width="100">
  <source src="demo.mp3" type="audio/mpeg">
  <source src="demo.ogg" type="audio/ogg">
  <embed height="50" width="100" src="demo.mp3">
</audio>
```

**讲解**

看到以上用到了三个标签，这样做的好处是audio会尝试用mp3 或 ogg 来播放音频，如果播放失败了，会回退到embed。

**效果**

显示的效果基本与audio一致！

![image-20220120231347590](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220120231347590.png)

## 3、audio标签

### 3.1、audio的属性

一些常用的audio属性，全局属性在这里就没有列出来来了。更多请到[w3school](https://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)查阅。

| 属性     | 描述                                               |
| :------- | :------------------------------------------------- |
| autoplay | 设置或返回是否在加载完成后随即播放音频/视频        |
| controls | 设置或返回音频/视频是否显示控件（比如播放/暂停等） |
| loop     | 设置或返回音频/视频是否应在结束时重新播放          |
| muted    | 设置或返回音频/视频是否静音                        |
| preload  | 设置或返回音频/视频是否应该在页面加载后进行加载    |
| src      | 设置或返回音频/视频元素的当前来源                  |

### 3.2、audio的事件

事件这是我们用来跟音频发生交互的重要武器。

同样的只给出部分事件，更多请到[w3school](https://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)查阅。

| 事件       | 描述                                        |
| ---------- | ------------------------------------------- |
| pause      | 当音频/视频已暂停时                         |
| play       | 当音频/视频已开始或不再暂停时               |
| playing    | 当音频/视频在已因缓冲而暂停或停止后已就绪时 |
| canplay    | 当浏览器可以播放音频/视频时                 |
| timeupdate | 当目前的播放位置已更改时                    |

## 4、来一个音频播放器的案例

讲了那么多，不就是等一个案例吗，来！

**码上！**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width,initial-scale=1 user-scalable=0" />
    <title>audio音频demo</title>
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

        #audio {
            width: 100%;
        }

        .control-body {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #control {
            width: 150px;
            height: 150px;
            border-radius: 200px;
            border: none;
            box-shadow: #888 0 0 8px;
        }

       
    </style>

</head>

<body>
    <script>

        function play() {
            let audio = document.getElementById("audio");
            if (audio.paused) {
                audio.pasue();
            } else {
                audio.play();
            }
        }

    </script>

    <h1>audio音频播放demo</h1>

    <div class="control-body">
        <button class="control" id="control" onclick="play()">开始</button>
    </div>

    <audio id="audio" src="http://96.ierge.cn/15/235/471737.mp3"></audio>

    

</body>

</html>
```

## 5、总结

音频的确在现在的网页中用的十分平常了，使用的的方式也发生了很大的改变。后续写一个关于音频的demo案例！

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







