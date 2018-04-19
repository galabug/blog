---
layout:     post
title:      "设计模式"
subtitle:   "本文是学习设计模式的笔记"
date:       2018-04-19
author:     "祝立健"
header-img: "img/v1/post-bg-universe.jpg"
tags:
    - java
    - 设计模式
    - 个人笔记
---


## 一、为什么学习设计模式

  学习利用其它开发人员的的智慧和经验。

## 二、设计原则：
1. 把需要变化的地方独立出来--**封装**起来，与不需要变化的代码分开。
2. 针对**接口编程**（针对超类编程，关键就在多态），而不是针对实现编程。
3. 



### 设计入门 
  ```java
      Duck() 鸭子类
    ----------------------------
    quack()
    swim()
    display()
    //鸭子的其他方法 <br>
    
  ```
-- 红头鸭，绿头鸭，玩具鸭。。。 
  
父类要增加飞行行为 fly()

  会对所有的子类产生影响 橡皮鸭
  ```java
      fly()// 后来新增
  ```
 

-- 使用接口
```java
 
    Duck() 鸭子类       Flyable接口       Quackable接口
  ---------------    ------------   ----------------------------
    swim()              fly()                 quack()
    display()
 

  Duck imp Flyable imp Qucackable
    //缺点： 子类重复实现各种功能
```
-- 使用超类作为鸭子类的属性
```java
  
    Duck() 鸭子类       Flyable飞行功能       Quackable
  ---------------    ---------------------    -------------------
    //属性                 
    Flyable                   fly()             quack()
    Quackable
    //方法
    swim()              
    display()
  
```






