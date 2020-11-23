---
title: "Java面向对象"
subtitle: ""
date: 2018-05-29
draft: true
author: "gaozhidong"

description: "Java面向对象"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

##### 对象

> - 对象的行为 ----可以对对象施加那些操作，或可以对对象施加那些方法？
> - 对象的状态 ----当施加那些方法时，对象如何响应？
> - 对象标识 ----如何辨别具有相同行为与状态的不同对象？


##### 类

> 类（class）是构造对象的模板。由类构造对象的过程称为创建类的是实例。

```
一个类以 public class开头，public class 代表这个类是公共类，类名必须和文件名相同 

public class Merchandise {
    //类体中可以定义描述这个类的属性的变量。 （成员变量）
    Sting name;
    String id;
    int count;
    double price;
}

public class SuperMarket{
    public static void main(String[] args){
        //使用new操作符，可以创建一个类的实例/对象（instance/object）
        //使用new创建一个类的实例后，类中定义的每种变量都会被赋以其类型的初始值。
    
        Merchandise m1 = new Merchandise();
        //赋值
        m1.name = "这是第一个name";
        m1.id = "000001";
        m1.count = 10000;
        m1.print = 88.8;
    }
} 
```



封装 继承 多态

> Java是一门面向对象的编程语言，除了基本数据类型以外，Java要求每一个数据类型必须都是一个类。
> <br/>面向对象的编程思想力图使在计算机语言中对事物的描述与现实世界中该事物的本来面目尽可能地一致，类（class）和对象（object）就是面向对象方法的核心概念。
> <br/>类是对某一类事物的描述，是抽象的、概念上的定义；对象是实际存在的该类事物的个体，因而也称实例（Instance）。类和对象就如同概念和实物之间的关系一样，类就好比是一个模板，而对象就是该模板下的一个实例。
> <br/>面向对象的主要思想是：将客观事物看作具有状态和行为的对象，通过抽象找出同一类对象的共同状态和行为，构成类。
> <br/> 在Java当中申明类都是由class开头的。



## 参考

[零基础学Java](https://time.geekbang.org/course/detail/181-97279)

