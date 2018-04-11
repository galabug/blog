---
layout:     post
title:      "前端网页性能 "
subtitle:   "本文将详细介绍性能问题的出现原因，以及解决方法。"
date:       2018-04-09
author:     "祝立健"
header-img: "img/v1/post-bg-universe.jpg"
tags:
    - 前端
    - 个人笔记
---


## 一、网页生成的过程

  要理解网页性能为什么不好，就要了解网页是怎么生成的。

  ![](https://galabug.github.io/img/v1/20180409/1.png)

  网页的生成过程，大致可以分成五步。
  ```js
    1.HTML代码转化成DOM
    2.CSS代码转化成CSSOM（CSS Object Model）
    3.结合DOM和CSSOM，生成一棵渲染树（包含每个节点的视觉信息）
    4.生成布局（layout），即将所有渲染树的所有节点进行平面合成
    5.将布局绘制（paint）在屏幕上
  ```
  这五步里面，第一步到第三步都非常快，耗时的是第四步和第五步。

  **"生成布局"（flow）和"绘制"（paint）这两步，合称为"渲染"（render）。**
  ![](https://galabug.github.io/img/v1/20180409/2.png)


  tips:
  1. js执行会阻塞DOM树的解析和渲染
  2. css加载不会阻塞DOM树的解析 
  3. css加载会阻塞DOM树的渲染 
  4. css加载会阻塞后面js语句的执行
  
  **优化1：（过时）**
  - css的引入在head中（让dom一渲染就有样式）
  - js的引入放在body后面，可以使页面展示出来的速度变快
  - 缺点：要等body解析完成后才去下载js，总体展示完整页面的时间稍微变长

  **优化2：**
  - 使用script标签的属性 async defer，让js的script的下载（只是下载不执行）和dom解析同时异步进行

  - defer:所有元素解析完成之后，才执行js，并且按script位置顺序，顺序执行，使用场景较多：相当于没有缺点的优化1
  ```js
    
    <script defer src="example.js"></script>

    <script defer src="example1.js"></script>

  ```

  - async：不能保证js的执行时间和顺序，使用场景较少
  ```js
    <script async src="example.js"></script>

    <script async src="example1.js"></script>
  ```
  下图可以直观的看出区别:
  ![](https://galabug.github.io/img/v1/20180409/3.jpg)

## 二、重排和重绘

  网页生成的时候，至少会渲染一次。用户访问的过程中，还会不断重新渲染。

  以下三种情况，会导致网页重新渲染。

  1. 修改DOM
  2. 修改样式表
  3. 用户事件（比如鼠标悬停、页面滚动、输入框键入文字、改变窗口大小等等）
  
  **重新渲染，就需要重新生成布局和重新绘制。前者叫做"重排"（reflow），后者叫做"重绘"（repaint）。**

  需要注意的是，**"重绘"不一定需要"重排"**，比如改变某个网页元素的颜色，就只会触发"重绘"，不会触发"重排"，因为布局没有改变。但是，**"重排"必然导致"重绘"**，比如改变一个网页元素的位置，就会同时触发"重排"和"重绘"，因为布局改变了。

## 三、对于性能的影响

  重排和重绘会不断触发，这是不可避免的。但是，它们非常耗费资源，是导致网页性能低下的根本原因。

  **提高网页性能，就是要降低"重排"和"重绘"的频率和成本，尽量少触发重新渲染。**

  前面提到，DOM变动和样式变动，都会触发重新渲染。但是，浏览器已经很智能了，会尽量把所有的变动集中在一起，排成一个队列，然后一次性执行，尽量避免多次重新渲染。

  ```js
    div.style.color = 'blue';
    div.style.marginTop = '30px';
  ```
  
  上面代码中，div元素有两个样式变动，但是浏览器只会触发一次重排和重绘。

  如果写得不好，就会触发两次重排和重绘。

  ```js
  div.style.color = 'blue';
  var margin = parseInt(div.style.marginTop);
  div.style.marginTop = (margin + 10) + 'px';
  ```
  上面代码对div元素设置背景色以后，第二行要求浏览器给出该元素的位置，所以浏览器不得不立即重排。

  一般来说，样式的写操作之后，如果有下面这些属性的读操作，都会引发浏览器立即重新渲染。
  ```js
  offsetTop/offsetLeft/offsetWidth/offsetHeight
  scrollTop/scrollLeft/scrollWidth/scrollHeight
  clientTop/clientLeft/clientWidth/clientHeight
  getComputedStyle()
  ```
  所以，从性能角度考虑，尽量不要把读操作和写操作，放在一个语句里面。

```js
  // bad
  div.style.left = div.offsetLeft + 10 + "px";
  div.style.top = div.offsetTop + 10 + "px";

  // good
  var left = div.offsetLeft;
  var top  = div.offsetTop;
  div.style.left = left + 10 + "px";
  div.style.top = top + 10 + "px";
  ```
  一般的规则是：
  ```js
  1.样式表越简单，重排和重绘就越快。
  2.重排和重绘的DOM元素层级越高，成本就越高。
  3.table元素的重排和重绘成本，要高于div元素
  ```
## 四、提高性能的九个技巧
  有一些技巧，可以降低浏览器重新渲染的频率和成本。

  **第一条**是上一节说到的，DOM 的多个读操作（或多个写操作），应该放在一起。不要两个读操作之间，加入一个写操作。

  **第二条**，如果某个样式是通过重排得到的，那么最好缓存结果。避免下一次用到的时候，浏览器又要重排。

  **第三条**，不要一条条地改变样式，而要通过改变class，或者csstext属性，一次性地改变样式。

  ```js
  // bad
  var left = 10;
  var top = 10;
  el.style.left = left + "px";
  el.style.top  = top  + "px";

  // good 
  el.className += " theclassname";

  // good
  el.style.cssText += "; left: " + left + "px; top: " + top + "px;";
  ```
  **第四条**，尽量使用离线DOM，而不是真实的网面DOM，来改变元素样式。比如，操作Document Fragment对象，完成后再把这个对象加入DOM。再比如，使用 cloneNode() 方法，在克隆的节点上进行操作，然后再用克隆的节点替换原始节点。

  **第五条**，先将元素设为display: none（需要1次重排和重绘），然后对这个节点进行100次操作，最后再恢复显示（需要1次重排和重绘）。这样一来，你就用两次重新渲染，取代了可能高达100次的重新渲染。

  **第六条**，position属性为absolute或fixed的元素，重排的开销会比较小，因为不用考虑它对其他元素的影响。

  **第七条**，只在必要的时候，才将元素的display属性为可见，因为不可见的元素不影响重排和重绘。另外，visibility : hidden的元素只对重绘有影响，不影响重排。

  **第八条**，使用虚拟DOM的脚本库，比如React等。

  **第九条**，使用 window.requestAnimationFrame()、window.requestIdleCallback() 这两个方法调节重新渲染

## 参考链接

  [阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/09/web-page-performance-in-depth.html)
  搬运过来的做个笔记
  
  [左正博客园](https://www.cnblogs.com/soundcode/p/5767812.html)