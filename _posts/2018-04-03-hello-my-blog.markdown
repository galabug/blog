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


### NPM 
> NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：
  - 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
  - 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
  - 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

* 新版的nodejs已经集成了npm

使用淘宝镜像的命令：
> cnpm install npm -g

### 使用 npm 命令安装模块

* npm 安装 Node.js 模块语法格式如下：

> npm install <Module Name>

* 以下实例，安装常用的 Node.js web框架模块 express:

> npm install express

* 安装好之后，express 包就放在了工程目录下的 node_modules 目录中，因此代码中只需要通过 require('express')使用。

> var express = require('express');

 ### 全局安装与本地安装

* npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有-g而已，比如
>  npm install express      # 本地安装
>  npm install express -g   # 全局安装
  - 本地安装
    1. 将安装包放在 ./node_modules 下（运行 npm 命令时所在的目录），如果没有 node_modules 目录，会在当前执行 npm 命令的目录下生成 node_modules 目录。
    2. 可以通过 require() 来引入本地安装的包。
  - 全局安装
    1. 将安装包放在 /usr/local 下或者你 node 的安装目录。
    2. 可以直接在命令行里使用。
* 如果出现以下错误：
> npm err! Error: connect ECONNREFUSED 127.0.0.1:8087 
* 解决办法为：
> npm config set proxy null

