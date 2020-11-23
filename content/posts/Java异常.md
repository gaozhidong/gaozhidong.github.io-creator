---
title: "Java异常"
subtitle: ""
date: 2018-08-13
draft: true
author: "gaozhidong"

description: "Java异常"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

### Java 异常

#### 异常是什么 ：

> Java异常是Java提供的一种识别及响应错误的一致性机制。是对问题的描述，将问题进行对象的封装。

#### 异常的好处：

> Java异常机制可以使程序中异常处理代码和正常业务代码分离，在有效使用异常
> 的情况下，异常能清晰的回答what,where,why这3个问题：异常类型回答了“什么
> ”被抛出，异常堆栈跟踪回答了“在哪“抛出，异常信息回答了“为什么“会抛出。

#### 异常两大体系：

异常类都是Throwable的子类。而在Throwable下有两个子类：

* Error：指的是JVM错误，指此时的程序还没有执行，如果没有执行用户无法处理。
* Exception：指的是程序运行中产生的异常，用户可以处理。

```
* Throwable （所有异常都是从Throwable继承而来。）
    * Error(错误，无毒)
    * Exception  - checked execption （受检异常，有毒，代表一种预料之中的异常，IOException）
         * RuntimeException （运行时异常，无毒，代表一种预料之外的异常，因此不需要声明）
* catch的级联与合并
```

#### 异常的抛出原则

* 能用if/else处理的，不要使用异常
* 尽早抛出异常
* 异常要准确、带有详细信息
* 抛出异常也比悄悄执行错误的逻辑强得多

#####  throw/throws

* throw  抛出一个异常，用于抛出异常。
* throws  只是一个声明，用在方法签名中，用于声明该方法可能抛出的异常。

#### 异常的处理原则

* 本方法是否有责任处理这个异常？
  * 不要处理不归自己管的异常
* 本方法是否有能力处理这个异常？
  * 如果自己无法处理，就抛出 
* 如非万分必要，不要忽略异常  

#### 异常的处理 try / catch / finally

* 如果没有try，异常将击穿所有的栈帧
* catch可以将一个异常抓住
* finally执行清理工作
* JDK7+： try-width-resources

```
try{
    // 有可能出现异常的语句
} [catch(异常类型 对象) {
    // 处理异常
} catch(异常类型 对象) {
    // 处理异常
} catch(异常类型 对象) {
    // 处理异常
} ... ] [finally {
    // 不管是否出现异常，都执行的统一代码
}]
```


##### JDK内置的异常

* NullPointerException (空指针异常) 

  * 调用了未经初始化的对象或者是不存在的对象

* ClassNotFoundException (指定的类不存在)

* NumberFormatException (字符串转换为数字异常)

  * 当试图将一个String转换为指定的数字类型，而该字符串确不满足数字类型要求的格式时，抛出该异常.如现在讲字符型的数据"111"转换为数值型数据时，是允许的。但是如果字符型数据中包含了非数字型的字符，"111aa111"转换为数值型时就会出现异常。系统就会捕捉到这个异常，并进行处理. 

* ClassCastException (数据类型转换异常)

* IllegalStateException

* IllegalArgumentException (方法的参数错误)

* IllegalAccessException (没有访问权限)

  * 当应用程序要调用一个类，但当前的方法即没有对该类的访问权限便会出现这个异常。对程序中用了Package的情况下要注意这个异常 

* IndexOutOfBoundsException (数组下标越界异常)

* ArithmeticException (数学运算异常)

* FileNotFoundException (文件未找到异常)

  * 当程序试图打开一个不存在的文件进行读写时将会引发该异常。该异常由FileInputStream,FileOutputStream,RandomAccessFile的构造器声明抛出。即使被操作的文件存在，但是由于某些原因不可访问，比如打开一个只读文件进行写入，这些构造方法仍然会引发异常

* ArrayStoreException (数组存储异常)

  * 当试图将类型不兼容类型的对象存入一个Object[]数组时将引发异常

  ```
   Object[] obj = new String[3];
  
   obj[0] = new Integer(0);
  ```

* NoSuchMethodException (方法不存在异常)

  * 当程序试图通过反射来创建对象，访问(修改或读取)某个方法，但是该方法不存在就会引发异常

* OutOfMemoryException (内存不足错误)

  * 当可用内存不足以让Java虚拟机分配给一个对象时抛出该错误。

* 等等