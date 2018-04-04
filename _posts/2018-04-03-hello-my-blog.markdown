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

### Node.js REPL(交互式解释器)
>Node.js REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。

Node 自带了交互式解释器，可以执行以下任务：
  - 读取 - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
  - 执行 - 执行输入的数据结构
  - 打印 - 输出结果
  - 循环 - 循环操作以上步骤直到用户两次按下 ctrl-c 按钮退出。

* 输入以下命令来启动 Node 的终端：
```js
 node
```

### Node.js 回调函数

