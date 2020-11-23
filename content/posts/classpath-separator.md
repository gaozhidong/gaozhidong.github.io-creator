---
title: "在windows 和 Unix 上calsspath separator 上是不同的"
subtitle: ""
date: 2018-08-17
draft: false
author: "gaozhidong"

description: "在windows 和 Unix 上calsspath separator 上是不同的"

tags: ["", ""]
categories: [""]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
**calsspath separator 在windows和Unix 上是不同的windows上是分号**


![file](/images/images-1.png)

![file](/images/image-junit.png)

1. 直接写java -cp .;junit-4.12.jar Main是会报错的，因为分号代表命令的结束，所以需要用引号括起来
2. shell不负责命令的解释，它会把这个path原封不动地交给java去处理
3. git bash 还是windows上的java，所以还是按照分号去分割，只能丢引号里传给java
4. 在unix系统里，分号用于分割两个shell命令
   **所以这个事情的坑爹之处就在于，git bash里的命令是遵循Unix系统的约定，但是传递给Java程序的classpath分隔符需要遵循windows系统的约定**

**另外：在cmd上不用引号**

#####  javac -cp junit-XXX.jar Main.java这个命令是什么

这个命令里，javac是executable，他的参数是classpath，Main.java是“即将被编译的文件”。Main.java中有一个ActiveTestSuite，那么这个类肯定不能从天上掉下来，要去哪儿找呢，就只能去-cp指定的地方找。

##### java命令 java -cp .;junit-XXX.java Main

Main代表“告诉JVM，要从Main类启动JVM”，那么Main类从哪儿找呢？只能从-cp指定的地方找。JVM运行Main的时候发现，这个引用了ActiveTestSuite，那这个类去哪儿找？也只能从-cp里找

