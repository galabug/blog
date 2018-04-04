---
layout:     post
title:      "我的博客开通了 "
subtitle:   "哈哈。"
date:       2018-04-03
author:     "zhulj"
header-img: "img/v1/post-bg-universe.jpg"
tags:
    - 生活
    - 个人笔记
---


> 终于折腾好了


---

* 可以写笔记了- --  -

### 开始学习node
  >  简单的说 Node.js 就是运行在服务端的 JavaScript。
  >  Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。
  >  Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。

* tip:检查环境变量，cmd中输入path

### Node.js 应用
* Node.js 应用由三部分组成：

    - 引入 required 模块：我们可以使用 require 指令来载入 Node.js 模块。
    - 创建服务器：服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。
    - 接收请求与响应请求 服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。

```js
    var http = require('http');

    http.createServer(function (request, response) {

        // 发送 HTTP 头部 
        // HTTP 状态值: 200 : OK
        // 内容类型: text/plain
        response.writeHead(200, {'Content-Type': 'text/plain'});

        // 发送响应数据 "Hello World"
        response.end('Hello World\n');
    }).listen(8888);

    // 终端打印如下信息
    console.log('Server running at http://127.0.0.1:8888/');
```
- 第一行请求（require）Node.js 自带的 http 模块，并且把它赋值给 http 变量。
- 接下来我们调用 http 模块提供的函数： createServer 。这个函数会返回 一个对象，这个对象有一个叫做 listen 的方法，这个方法有一个数值参数， 指定这个 HTTP 服务器监听的端口号。


### NPM [NPM是随同NodeJS一起安装的包管理工具](https://galabug.github.io/2018/04/04/js-node-npm/)

### Node.js 全局对象:它及其所有属性都可以在程序的任何地方访问
  - JavaScript 中有一个特殊的对象window，称为全局对象
  - Node.js 中的全局对象是 global，

##### 全局对象与全局变量
  * global 最根本的作用是作为全局变量的宿主。
    - 在最外层定义的变量；
    - 全局对象的属性；
    - 隐式定义的变量（未定义直接赋值的变量）。
  >当你定义一个全局变量时，这个变量同时也会成为全局对象的属性，反之亦然。需要注 意的是，在 Node.js 中你不可能在最外>层定义变量，因为所有用户代码都是属于当前模块的， 而模块本身不是最外层上下文。

  > **注意： 永远使用 var 定义变量以避免引入全局变量，因为全局变量会污染 命名空间，提高代码的耦合风险。**

1. **__filename**
  >表示当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。 如果在模块中，返回的值是模块文件的路径。

2. **__dirname**
  >表示当前执行脚本所在的目录。

3. setTimeout(cb, ms)  clearTimeout(t)  setInterval(cb, ms)  clearInterval(t) 
  > 同js

4. console 


5. process  
  >用于描述当前Node.js 进程状态的对象，提供了一个与操作系统的简单接口。通常在你写本地命令行程序的时候，少不了要 和它打交道。
##### 下面将会介绍 process 对象的一些最常用的成员方法。
  - exit
    当进程准备退出时触发。
  - beforeExit
    当 node 清空事件循环，并且没有其他安排时触发这个事件。通常来说，当没有进程安排时 node 退出，但是 'beforeExit' 的监听器可以异步调用，这样 node 就会继续执行。
  - uncaughtException
    当一个异常冒泡回到事件循环，触发这个事件。如果给异常添加了监视器，默认的操作（打印堆栈跟踪信息并退出）就不会发生。
  -	Signal 事件
    当进程接收到信号时就触发。信号列表详见标准的 POSIX 信号名，如 SIGINT、SIGUSR1 等。

    Process 属性

##### Process 提供了很多有用的属性，便于我们更好的控制系统的交互：

  1. stdout
    > 标准输出流。
  2. 	stderr
    > 标准错误流。
  3.	stdin
    > 标准输入流。
  4.	argv
    > argv 属性返回一个数组，由命令行执行脚本时的各个参数组成。它的第一个成员总是node，第二个成员是脚本文件名，其余成员是脚本文件的参数。
  5.	execPath
    > 返回执行当前脚本的 Node 二进制文件的绝对路径。
  6.	execArgv
    > 返回一个数组，成员是命令行下执行脚本时，在Node可执行文件与脚本文件之间的命令行参数。
  7.	env
    > 返回一个对象，成员为当前 shell 的环境变量
  8.	exitCode
    > 进程退出时的代码，如果进程优通过 process.exit() 退出，不需要指定退出码。
  9.	version
    > Node 的版本，比如v0.10.18。
  10.	versions
    > 一个属性，包含了 node 的版本和依赖.
  11.	config
    > 一个包含用来编译当前 node 执行文件的 javascript 配置选项的对象。它与运行 ./configure 脚本生成的 "config.gypi" 文件相同。
  12.	pid
    > 当前进程的进程号。
  13.	title
    > 进程名，默认值为"node"，可以自定义该值。
  14.	arch
    > 当前 CPU 的架构：'arm'、'ia32' 或者 'x64'。
  15.	platform
    > 运行程序所在的平台系统 'darwin', 'freebsd', 'linux', 'sunos' 或 'win32'
  16.	mainModule
    > require.main 的备选方法。不同点，如果主模块在运行时改变，require.main可能会继续返回老的模块。可以认为，这两者引用了同一个模块。

### Node.js Express 框架
  Express 简介
  > Express 是一个简洁而灵活的 node.js Web应用框架, 提供了一系列强大特性帮助你创建各种 Web 应用，和丰富的 HTTP 工具。

  Express 框架核心特性：
  - 可以设置中间件来响应 HTTP 请求。
  - 定义了路由表用于执行不同的 HTTP 请求动作。
  - 可以通过向模板传递参数来动态渲染 HTML 页面。

  * 安装 Express
  * 安装 Express 并将其保存到依赖列表中：
```js
  cnpm install express --save
```


