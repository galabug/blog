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



### 二、设计入门 
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
      fly()// 新增
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
  
    Duck() 鸭子类       FlyBehavior飞行功能       QuackBehavior呱呱叫功能
  ---------------    ---------------------    -------------------
    //属性                 
    FlyBehavior             fly()              quack()
    QuackBehavior
    //方法
    swim()              
    display()
    performFly(){
      FlyBehavior.fly()
    }
    QuackBehavior(){
      QuackBehavior.quack()
    }
  
```

-- 整合
```java
  MallardDuck extends Duck{
    public MallarDuck(){
      quackBehavior = new Duck();
      flyBehavior = new FlyWithWings();
    }

    Getter...
    Setter...
  }
```
### 2.1 策略模式：定义了算法族，分别封装起来，让他们之间可以相互替换，此模式让算法的变化独立于使用算法的对象
  
-- 上面的例子采用的就是策略模式


### 2.2 观察者模式Observer：定义了对象之间的一对多依赖。当一个对象发生状态改变，它的所有依赖者都会收到通知并自动更新。

```java

  <interface>               <interface> 
  Subject                 Observer
  ---------------------   -------------------------
  registerObserver()        update()
  removeObserver()        
  notifyObserver()        



public class WeatherData implements Subject{
    private ArrayList observers;
    private float temp;
    private float humidity;
    private float pressure;
    public WeatherData(){
      this.observers=new Arraylist();
    }
    public void registerObserver(Observer o){
      observers.add(o);
    }      
    public void removeObserver(Observer o){
      int i = observers.indexOf(o);
      if(i>0){
          observers.remove(i);
      }
    }        
    public void notifyObserver(){
      for(int i=0,s=observers.size();i<s;i++>){
        Observer ob=(Observer)observers.get(i);
        ob.update(temp,humidity,pressure);
      }
    }  

    public void changed(){
      notifyObserver();
    }
    // 其他方法 
} 

public class Display implements Observer{
    private Subject weatherData;
    private float temp;
    private float humidity;
    private float pressure;

    public Display(Subject weatherData){
      this.weatherData=weatherData;
      weatherData.registerObserver(this);
    }
    public void update(float temp,float humidity,float pressure){

    }
}  
```

###### java API内置的观察者模式，java.util包里Observer接口和Observable类。

###### 可观察者：继承java.util.Observable，产生可观察者，然后
  1. 先调用setChange()方法，标记状态已经改变的事实。
  2. 然后调用两种notifyObservers()方法
    - notifyObservers()  
    - notifyObservers(Object arg) -->传送任何数据对象给每一个观察者
###### 观察者：实现java.util.Observer接口，产生观察者
  - update(Observable o,Object arg);
  - o:主题本身当做一个参数，让观察者知道哪个主题通知了它
  - arg:传入的数据对象，如果没有说明则为空
###### push:通过arg主题把数据推给观察者，pull：观察者也可以直接从o主题对象直接获取想要的数据--拉

```java

public class WeatherData implements Observable{
    private float temp;
    private float humidity;
    private float pressure;
    public WeatherData(){
    }
   
    public void changed(){
      setChanged();
      notifyObservers();
    }

    public void setTemp(float temp,float humidity,float pressure){
      this...
      changed();
    }
    // 其他方法    
}                


public class Display implements Observer{
    private Observable observable;
    private float temp;
    private float humidity;
    private float pressure;

    public Display(Observable observable){
      this.observable=observable;
      observable.addObserver(this);
    }
    public void update(Observable obs,Object args){
      if(obs instanceof WeatherData){
        WeatherData wea=(WeatherData)obs;
        this...

      }
    }

}  

 ```


### 2.3 装饰者模式：动态地将责任附加到对象上。要扩展功能，装饰者提供有利于继承的另一种选择。

- JAVA I/O类
```java



```
### 2.4 工厂方法模式：定义了一个创建对象的接口，但子类决定要实例化的类是哪一个。工厂方法让类 把实例化推迟到子类。
- 一种类似模式的编程习惯：简单工厂模式。
- 工厂方法用来处理对象的创建，并将这样的行为封装在子类中。这样，关于超类的代码就和子类对象的创建代码解耦了。
- 工厂方法模式Factory Method Pattern 通过让子类决定如何创建对象，来将对象的创建过程封装。注意：这里的‘决定’是指，选择了哪个子类，自然就决定了实际创建的产品是什么。


### 2.5 单例模式：确保一个类只能创建一个实例，并提供全局访问点。

```java
public class Singleton{
  private static Singleton uniqueInstance;
  private Signleton(){}//私有化构造函数
  public static Sinleton getInstance(){//提供全局访问点
    if(uniqueInstance==null){
        uniqueInstance=new Singleton();
    }
    return uniqueInstance;
  }
}
//***********多线程时上面有问题*************

//***********synchronized能解决多线程问题，但是会降低性能*************
public class Singleton{
  private static Singleton uniqueInstance;
  private Signleton(){}//私有化构造函数
  public static synchronized Sinleton getInstance(){//提供全局访问点
    if(uniqueInstance==null){
        uniqueInstance=new Singleton();
    }
    return uniqueInstance;
  }
}

//***********JVM加载类时，初始化实例*************
public class Singleton{
  private static Singleton uniqueInstance=new Singleton();
  private Signleton(){}//私有化构造函数
  public static Sinleton getInstance(){//提供全局访问点
    return uniqueInstance;
  }
}

//双重检查加锁 java1.5以上
public class Singleton{
  private static volatile uniqueInstance;
  private Signleton(){}//私有化构造函数
  public static Sinleton getInstance(){//提供全局访问点
    if(uniqueInstance==null){
        synchronized(Singleton.class){
          if(uniqueInstance==null){
              uniqueInstance=new Singleton();
          }
        }
    }
    return uniqueInstance;
  }
}

```
### 2.6 命令模式：将“请求”封装成对象，以便使用不同的请求、队列或者日志来参数化其他对象。命令模式支持可撤销的操作。



### 2.7 适配器模式：将一个类的接口，转换成客户期望的另一个接口。让原本接口不兼容的类可以合作无间。



## 三、设计原则：
1. 把需要变化的地方独立出来--**封装**起来，与不需要变化的代码分开。
2. 针对**接口编程**（针对超类编程，关键就在多态），而不是针对实现编程。
3. 多用组合，少用继承。“有一个”关系比“是一个”更好。（把两个或以上类结合起来使用--组合composition）。
4. 为了交互对象之间的松耦合设计而努力。
5. 类应该对扩展开放，对修改关闭。
6. 要依赖抽象，不要依赖具体类。

## tips

  -- 面向对象之路重要的是**复用**。
  -- 软件开发后通常比软件开发前花的时间更多，因此我们应该致力于提高可维护性和可扩展性的复用程度。
  -- 模式只不过是利用OO设计原则？？
  -- 知道封装、抽象、继承、多态，并不会让你马上变成好的面向对象设计者。
  -- 设计大师关心的是建立弹性的设计，可以维护，可以应付变化。
  -- 建立可维护的的OO系统，要诀：**
 
  **




































