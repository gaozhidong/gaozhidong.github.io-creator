---
title: "Java基本结构"
subtitle: ""
date: 2018-04-25
author: "gaozhidong"

description: "java基本结构"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
* java基本结构 从上到下分为:

**包** 
** 类** （存放代码基本单元），
类中包含： **  静态成员**  **  静态方法**  **  实例变量 **  **  实例方法**  



####  静态变量

存放在jvm中全局的存储单元， 被所有的有访问权限的对象共享。

#### 静态方法

静态方法可以直接通过类名调用，任何的实例也都可以调用

#### 实例方法

通过对象的实例来调用。

#### 成员变量

和一个对象绑定


在自己类内部可以直接访问 静态变量和静态方法，再别的类中，必须加上类型来访问