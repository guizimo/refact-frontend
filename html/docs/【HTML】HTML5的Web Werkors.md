# 【HTML】HTML5的Web Werkors

## 引言

内容速递：看了本文您能了解到的知识！

![HTML5的Web worlers](https://guizimo.oss-cn-shanghai.aliyuncs.com/img/HTML5%E7%9A%84Web%20worlers.png)

## 1、什么是Web workers

JavaScript 语言采用的是单线程模型，也就是说，所有任务只能在一个线程上完成，一次只能做一件事。前面的任务没做完，后面的任务只能等着。

随着电脑计算能力的增强，尤其是多核 CPU 的出现，单线程带来很大的不便，无法充分发挥计算机的计算能力。

## 2、Web Workers使用场景

Workers线程可以执行任务而不干扰用户界面。一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，这就是Web Workers出现的意义了。

## 3、Web Workers的使用条件

（1）**同源限制**

分配给 Worker 线程运行的脚本文件，必须与主线程的脚本文件同源。

（2）**DOM 限制**

Worker 线程所在的全局对象，与主线程不一样，无法读取主线程所在网页的 DOM 对象，也无法使用`document`、`window`、`parent`这些对象。但是，Worker 线程可以`navigator`对象和`location`对象。

（3）**通信联系**

Worker 线程和主线程不在同一个上下文环境，它们不能直接通信，必须通过消息完成。

（4）**脚本限制**

Worker 线程不能执行`alert()`方法和`confirm()`方法，但可以使用 XMLHttpRequest 对象发出 AJAX 请求。

（5）**文件限制**

Worker 线程无法读取本地文件，即不能打开本机的文件系统（`file://`），它所加载的脚本，必须来自网络。

## 4、Web Workers实例

### 4.1、主线程操作

**1、检测浏览器是否支持 Web Worker**

判断兼容性，是否支持Web Workers

```javascript
if (window.Worker) {
	...
}
```

**2、创建Worker**

主线程采用`new`命令，调用`Worker()`构造函数，新建一个 Worker 线程。

```javascript
var myWorker = new Worker('worker.js');
```

**3、向Worker发送消息和接收Worker的消息**

主线程调用`worker.postMessage()`方法，向 Worker线程 发消息。发送的消息可以是各种数据类型，number，string，boolean ，file，blob 等。

```javascript
worker.postMessage('Hello World');
```

主线程通过`worker.onmessage`指定监听函数，接收 Worker线程发回来的消息。

```javascript
worker.onmessage = function (event) {
  console.log('Received message ' + event.data);
}
```

**4、关闭Worker**

Worker 线程完成任务以后，主线程就可以把它关掉。

```javascript
worker.terminate();
```

**5、异常处理**

可以通过`onerror`来捕获worker的异常

```javascript
worker.onerror = function () {
	console.log('There is an error with your worker!');
}
```

### 4.2、Worker 线程操作

**1、内部监听函数**

Worker 线程内部需要有一个监听函数，监听`message`事件。

```javascript
addEventListener('message', function (e) {
  postMessage('worker said: ' + e.data);
}, false);
```

除了使用`addEventListener()`指定监听函数，也可以使用`onmessage`指定。

```javascript
onmessage = function (e) {
  postMessage('worker said: ' + e.data);
};
```

**2、向主线程发送数据**

同样的， Worker线程调用`postMessage()`方法，向主线程发消息。

```javascript
postMessage('my worker');
```

**3、结束线程**

Worker 线程完成任务以后，自身也可调用`close()`关闭。

```javascript
close()
```

**4、异常处理**

Worker 线程完自身也可通过`onerror`监听错误信息。

```javascript
onerror = function (err) {
   console.log(err)
}   
```

**5、引入脚本**

Worker 内部如果要加载其他脚本，有一个专门的方法`importScripts()`。

```javascript
importScripts('script1.js');
```

该方法可以同时加载多个脚本。

```javascript
importScripts('script1.js', 'script2.js');
```

## 5、一个完整的实例

**主线程main.js**

```javascript
if (window.Worker) {   //兼容性判断。
    //创建一个worker线程。
    const worker = new Worker("worker.js");
    //向worker线程发送数据
    worker.postMessage('hello world');
 	//监听后台任务，
    worker.onmessage = function (e) {
        result.textContent = e.data;
     	console.log('Message received from worker');
    }
	//当myWorker异常时的时候会触发onerror事件    
	myWorker.onerror = function () {
        console.log('There is an error with your worker!');
    }
} else { 
    console.log('Your browser doesn\'t support web workers.')
}
```

**Worker线程worker.js**

```javascript
//监听主线程
onmessage = function (e) {
	console.log('Worker: Message received from main script');
    //接收来自主线程发送过来的数据
    let res = e.data;
	//2.向主线程发送数据
    postMessage('任务完成啦！')
}
    
//在worker线程中也可以监听错误信息。
onerror = function (err) {
    console.log(err)
}
```

## 6、Web Workers API

### 6.1、主线程

用来供主线程操作 Worker线程的API。

- Worker.onerror：指定 error 事件的监听函数。
- Worker.onmessage：指定 message 事件的监听函数，发送过来的数据在`Event.data`属性中。
- Worker.onmessageerror：指定 messageerror 事件的监听函数。发送的数据无法序列化成字符串时，会触发这个事件。
- Worker.postMessage()：向 Worker 线程发送消息。
- Worker.terminate()：立即终止 Worker 线程。

### 6.2、Worker线程

Web Worker 有自己的全局对象，不是主线程的`window`，Worker 线程有一些自己的全局属性和方法。

- self.name： Worker 的名字。该属性只读，由构造函数指定。
- self.onmessage：指定`message`事件的监听函数。
- self.onmessageerror：指定 messageerror 事件的监听函数。发送的数据无法序列化成字符串时，会触发这个事件。
- self.close()：关闭 Worker 线程。
- self.postMessage()：向产生这个 Worker 线程发送消息。
- self.importScripts()：加载 JS 脚本。

## 7、对Worker的一些思考

**1、既然是多线程了，那么关于线程安全问题值得思考**

Web Worker 与其他线程的通信其实是被严格控制起来的，没有办法去访问非线程安全的组件或者是 DOM。

官方话语：**你要是不费点劲儿，还真搞不出错误来。**

**2、Worker 中接收与发送的数据**

在主页面与 worker 之间传递的数据是通过**拷贝**，而不是共享来完成的。传递给 `Worker  `的对象需要经过序列化，接下来在另一端还需要反序列化。

**3、Worker中在创建Worker**

Worker中在创建Worker只在部分浏览器中使用，兼容性差，不推荐使用。

**4、将Ajax轮询放在Worker线程里面**

ajax 属于是异步操作，在浏览器中有自己的线程，而且兼容性很好。如果使用Worker的话，需要考虑到浏览器对Worker的兼容性。结合来看的话，不必要放在Worker里面。

## 8、总结

Web Werkors让浏览器能够参与更多的工作。新的技术感觉可以去尝试！

## 博客说明与致谢

> 文章所涉及的部分资料来自互联网整理，其中包含自己个人的总结和看法，分享的目的在于共建社区和巩固自己。
>
> 引用的资料如有侵权，请联系本人删除！
>
> 感谢勤劳的[自己](https://www.guizimo.com)，[个人博客](https://blog.guizimo.com/)，[GitHub学习](https://github.com/Tangleia)，[GitHub](https://github.com/guizimo)
>
> 公众号[【归子莫】](https://welcome.guizimo.com/gzh)，小程序[【子莫说】](https://welcome.guizimo.com/zms)
>
> 如果你感觉对你有帮助的话，不妨给我点赞鼓励一下，好文记得收藏哟！关注我一起成长！
>
> 幸好我在，感谢你来！

