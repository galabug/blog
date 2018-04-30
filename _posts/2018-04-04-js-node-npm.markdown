---
layout:     post
title:      "NPM "
subtitle:   "熟悉下markdown"
date:       2018-04-04
author:     "zhulj"
header-img: "img/v1/post-bg-universe.jpg"
tags:
    - javascript
    - 个人笔记
---



---


### NPM 
> NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：
  - 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
  - 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
  - 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

* 新版的nodejs已经集成了npm

使用淘宝镜像的命令：
> npm install cnpm -g

#### 使用 npm 命令安装模块

* npm 安装 Node.js 模块语法格式如下：

> npm install <Module Name>

* 以下实例，安装常用的 Node.js web框架模块 express:

> npm install express

* 安装好之后，express 包就放在了工程目录下的 node_modules 目录中，因此代码中只需要通过 require('express')使用。

> var express = require('express');

#### 全局安装与本地安装
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

#### 查看安装信息
  * 查看所有全局安装的模块：
    > npm list -g
  * 查看某个模块的版本号：
    > npm list <moduleName>

#### 使用 package.json   
- Package.json 属性说明
- name - 包名。
- version - 包的版本号。
- description - 包的描述。
- homepage - 包的官网 url 。
- author - 包的作者姓名。
- contributors - 包的其他贡献者姓名。
- dependencies - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。
- repository - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。
- main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
- keywords - 关键字

**卸载模块**

我们可以使用以下命令来卸载 Node.js 模块。
>npm uninstall express
卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：
>npm ls

**更新模块**

我们可以使用以下命令更新模块：
>npm update express

**搜索模块**

使用以下来搜索模块：

>npm search express

**创建模块**

创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

> npm init

淘宝定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

> npm install -g cnpm --registry=https://registry.npm.taobao.org
这样就可以使用 cnpm 命令来安装模块了：

>cnpm install [name]