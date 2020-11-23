---
title: "Java包管理"
subtitle: ""
date: 2018-09-09
draft: false
author: "gaozhidong"

description: "Java包管理"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

#####  什么是包

* Class（类）是 Java 中的一等公民，所有的 Java 代码，都要写在类里面
* 在命名规则下，你可以给类起任何名字。当你使用别人的类时，首先知道的是类名，然后再了解如何使用这个类。
* 随着人们编写的 Java 类越来越多，就会有个问题：如果出现了名字相同的类怎么办？两个名字相同的 User 类，其内涵是否也一样呢？如果不一样，要如何区分它们呢？

**Package** （包）就是用来解决这个问题的。通过将同名的类放到不同的包里面，我们就可以：

1. 对同名的类进行区分；
2. 精确地指明我们需要其中的哪一个；
3. 让同名的类在一个程序当中共存。 

###### JVM的工作被设计地相当简单：

1. 执行一个类的字节码 
2. 假如这个过程中碰到了新的类，加载它 
3. 那么，去哪里加载这些类呢？

类路路径（Classpath）

```
//可以包含多个可供选择的查询路径。每个路径都用分号隔开
-classpath /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/charsets.jar
```

类的全限定类名（目录层级）唯一确定了一个类

包就是把许多类放在一起的压缩包!

* 传递性依赖

你依赖的类还依赖了别的类，JVM只认类的说明书（字节码），你要使用一个库，你就得想办法把这份说明书以及它引用的说明书（传递性依赖）找到，然后给JVM。

看上去不是非常困难是不是？想象一下你的程序运行需要一万份说明书吧（传递性依赖的传递性依赖的传递性依赖）

Classpath hell 

全限定类名是类的唯一标识 

当多个同名类同时出现在Classpath中，就是噩梦的开始


##### 什么是包管理

你要使用一些第三方类，总要告诉JVM从哪里找

包管理的本质就是告诉JVM如何找到所需的第三方类库以及成功地解决其中的冲突问题!


##### 包管理发展历程

* 手动写命令进行编译运行


* Apache Ant 

1. 手动下载jar包，放在一个目录中 

2. 写XML配置，指定编译的源代码目录、依赖的jar包、输出目录等 

 **缺点** 

1. 每个人都要自己造一套轮子 

2. 依赖的第三方类库都需要手动下载，费时费力 

3. 假如你的应用依赖了了一万个第三方的类库呢？

4. 没有解决Classpath地狱的问题


* Maven 

1. Convention over configuration 

2. 约定优于配置 

3. 必须强调，Maven远远不止是包管理工具 

4. Maven的中央仓库 

5. 按照一定的约定存储包 

6. Maven的本地仓库 默认位于~/.m2 

7. 下载的第三方包放在这里进行缓存


**Maven的包**

1. 按照约定为所有的包编号，方便检索  groupId/artifactId/version 
2. 传递性依赖的自动管理 

**原则**：

* 绝对不允许最终的classpath出现同名不不同版本的jar包 
* 依赖冲突的解决：原则：最近的胜出 
* 依赖的scope 

**当你看到如下的异常的时候**

* AbstractMethodError 
* NoClassDefFoundError 
* ClassNotFoundException 
* LinkageError