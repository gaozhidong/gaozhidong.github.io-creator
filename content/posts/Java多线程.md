---
title: "Java多线程"
subtitle: ""
date: 2019-05-21
draft: true
author: "gaozhidong"

description: "Java 多线程"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

#### 进程和线程

> 线程（英语：thread）是操作系统能够进行运算调度的最小单位。大部分情况下，它被包含在进程之中，是进程中的实际运作单位。一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并行多个线程，每条线程并行执行不同的任务。在Unix System V及SunOS中也被称为轻量进程（lightweight processes），但轻量进程更多指内核线程（kernel thread），而把用户线程（user thread）称为线程。

> 一个进程可以有很多线程，每条线程并行执行不同的任务。

#### Java线程

> 最简单的情况是，Thread/Runnable的run()方法运行完毕，自行终止。

Java中创建线程的方式有两种，不管使用继承Thread的方式还是实现Runnable接口的方式，都需要重写run方法。

```
//继承Thread类
1、 定义继承Thread;

2、复写Thread类中的run方法;（目的：将自定义代码存储在run方法中，让线程运行（同时运行，抢夺资源））

3、调用线程的start方法；（目的：启动线程，调用run方法）

//实现Runnable接口
1、定义类实现Runnable接口；
  
2、覆盖Runnable接口中的run方法；

3、通过Thread类建立线程对象；

4、将Runnable接口的子类对象作为实际参数传递给Thread类的构造方法；

5、调用Thread类的start方法，开启线程并调节Runnable接口子类的run方法；
  
  
//区别：
继承只能继承一个，具有局限性。
继承Thread: 线程代码存放在子类run。
实现runnable: 线程代码存放在接口的子类run。
```

> 对于更复杂的情况，比如有循环，则可以增加终止标记变量和任务终止的检查点。

> 最常见的情况，也是为了解决阻塞不能执行检查点的问题，用中断来结束线程，但中断只是请求，并不能完全保证线程被终止，需要执行线程协同处理。

> IO阻塞和等锁情况下需要通过特殊方式进行处理。

> 使用Future类的cancel()方法调用。

> 调用线程池执行器的shutdown()和shutdownNow()方法。

> 守护线程会在非守护线程都结束时自动终止。

> Thread有stop()方法，但已不推荐使用。


#### Java中进程与线程的关系：

1. 运行一个程序会产生一个进程，进程至少包含一个线程。
2. 每个进程对应一个JVM实例，多个线程共享JVM中的堆。
3. Java采用单线程编程模型，程序会自动创建主线程。
4. 主线程可以创建子线程，原则上要后于子线程完成执行。

**多线程**

即便处理器只能运行一个线程，操作系统也可以通过快速的在不同线程之间进行切换，由于时间间隔很小，来给用户造成一种多个线程同时运行的假象。这样的程序运行机制被称为软件多线程。



### 为什么需要多线程

* 现代CPU都是多核的
* Java执行模型是同步/阻塞(block)的
* 默认情况下只有一个进程
  * 处理问题非常自然
  * 但是具有严重的性能问题

#### 开启一个新的线程

##### Thread

* Java中只有这么一种东西代表线程
* start方法才能并发执行
* 每多开一个线程，就多一个执行流
* 方法栈（局部变量）是线程私有的
* 静态方法/类变量是被所有线程共享的


##### 多线程带来的性能提升

* 对于IO密集型应用及其有用
  * 网络IO （通常包括数据库）
  * 文件IO
* 对于CUP密集型应用稍有折扣
* 性能提升的上线在哪里？
  * 单核CPU 100%
  * 多核CUP N * 100%

##### 昂贵的线程

* 能不能使用线程达到无穷无尽的性能提升?
* 线程的昂贵性在于
  * CPU切换上下文很慢
  * 线程需要占用内存等系统资源
* 如果应用一天才几个用户
  * new Thread().start()
* 如果应用负载很高
  * 使用线程池： JUC包 

##### 线程安全

* 原子性
* 共享变量
* 默认的实现几乎都不是线程安全的

##### 线程不安全的表现

* 数据错误
  * i++
  * if-then-do
* 死锁


##### 线程安全

* 实现线程安全的基本手段
  * 不可变类
    * Integer/String 
* synchronized 同步块
* JUC包
  * AtomicInteger
  * ConcurrentHashMap
    * 任何使用HashMap有线程安全问题的地方，都无脑使用ConcurrentHashMap替换即可
  * ReentrantLock
  * ...

##### 线程池与Callable/Future

* 什么是线程池
  * 线程池是昂贵的（Java线程模型的缺陷）
  * 线程池是预先定义好的若干个线程
  * Java中的线程池
* Callable/Future
  * 类比Runnable，Callable可以返回值，抛出异常
  * Future代表一个“未来才会返回的结果”

##### 多线程的经典问题

**生产者/消费者模型**

* 解决方法： 
  * wait/notify/notifyAll
  * Lock/Condition
  * BlockingQueue