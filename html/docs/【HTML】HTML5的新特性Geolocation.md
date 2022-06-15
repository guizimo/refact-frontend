# 【HTML】HTML5的新特性Geolocation

## 引言

内容速递：看了本文您能了解到的知识！

![HTML5定位](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E5%AE%9A%E4%BD%8D.png)

位置是个人隐私，但技术得学习！

**官方介绍：**

HTML5 Geolocation API 用于获得用户的地理位置。

鉴于该特性可能侵犯用户的隐私，除非用户同意，否则用户位置信息是不可用的。

## 1、获取物理定位

查看浏览器中是否有`navigator.geolocation`对象，有的话说明支持定位。

在这个对象下有一个getCurrentPosition()，可以获取当前的经度和纬度。

![image-20220223151422309](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220223151422309.png)

### 1.1、getCurrentPosition()

**语法**

```js
navigator.geolocation.getCurrentPosition(success, error, options)
```

**参数**

- *success*

  成功得到位置信息时的回调函数，使用`Position`]对象作为唯一的参数。 

- *error* 可选

  获取位置信息失败时的回调函数，使用 `PositionError`]对象作为唯一的参数，这是一个可选项。 

- *options* 可选

  一个可选的`PositionOptions`对象。

### 1.2、成功回调

getCurrentPosition()接受第一个参数是一个方法，也就是获取地址成功的回调。

```js
navigator.geolocation.getCurrentPosition((e) => {console.log(e)})
```

首先回询问你，是否授予权限。

![image-20220223153606103](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220223153606103.png)

在浏览器的执行截图

![image-20220223154150290](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220223154150290.png)

可以看到，已经成功获取了经纬度。

**获取成功的数据**

| 属性                    | 描述                   |
| :---------------------- | :--------------------- |
| coords.latitude         | 十进制数的纬度         |
| coords.longitude        | 十进制数的经度         |
| coords.accuracy         | 位置精度               |
| coords.altitude         | 海拔，海平面以上以米计 |
| coords.altitudeAccuracy | 位置的海拔精度         |
| coords.heading          | 方向，从正北开始以度计 |
| coords.speed            | 速度，以米/每秒计      |
| timestamp               | 响应的日期/时间        |

### 1.3、异常回调

当然异常的场景还是需要我们自己来模拟，接收第二个参数。

```js
navigator.geolocation.getCurrentPosition((e) => {console.log(e),(e) => {console.log(e)}})
```

在弹出授权的窗口中，选择禁止！可以看到返回的的错误信息。

![image-20220223155657095](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/image-20220223155657095.png)

> 错误代码
>
> - Permission denied - 用户不允许地理定位
> - Position unavailable - 无法获取当前位置
> - Timeout - 操作超时

## 2、一个获取物理定位的实例

结合成功回调和异常回调

```js
var options = {
  enableHighAccuracy: true,
  timeout: 5000,
  maximumAge: 0
};

// 成功回调
function success(pos) {
  var crd = pos.coords;
  console.log('位置信息:');
  console.log('Latitude : ' + crd.latitude);
  console.log('Longitude: ' + crd.longitude);
};

// 失败回调
function error(err) {
  console.warn('ERROR(' + err.code + '): ' + err.message);
};

navigator.geolocation.getCurrentPosition(success, error, options);
```

## 3、监听地址变化

在前端打印`navigator.geolocation`对象的时候，发现还有其他两个方法：watchPosition()和clearWatch()。

### 3.1、watchPosition() 

返回用户的当前位置，并继续返回用户移动时的更新位置（就像汽车上的 GPS）。

**语法**

```js
id = navigator.geolocation.watchPosition(success, error, options)
```

**参数**

- *success*

  成功时候的回调函数， 同时传入一个 `Position`对象当作参数。

- *error* 可选

  失败时候的回调函数，可选， 会传入一个 `PositionError`对象当作参数。

- *options* 可选

  一个可选的 `PositionOptions` 对象。

### 3.2、clearWatch()

 停止 watchPosition() 方法

**语法**

```js
navigator.geolocation.clearWatch(id);
```

参数

**id**

- 希望移除的监听器所对应的 `Geolocation.watchPosition()`返回的 ID 数字。

### 3.3、实例

```js
var id, target, option;

// 成功回调
function success(pos) {
  var crd = pos.coords;
  if (target.latitude === crd.latitude && target.longitude === crd.longitude) {
    console.log('到达目的地！');
    navigator.geolocation.clearWatch(id);
  }
};

// 错误处理
function error(err) {
  console.warn('ERROR(' + err.code + '): ' + err.message);
};

// 目标经纬度
target = {
  latitude : 0,
  longitude: 0,
}

options = {
  enableHighAccuracy: false,
  timeout: 5000,
  maximumAge: 0
};

id = navigator.geolocation.watchPosition(success, error, options);
```

## 4、总结

Geolocation的三个最基本的方法`getCurrentPosition`、`clearWatch`、`watchPosition`需要记住哈！

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







