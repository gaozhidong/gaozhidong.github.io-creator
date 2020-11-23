---
title: "Java程序运行流程"
subtitle: ""
date: 2018-09-19
draft: true
author: "gaozhidong"

description: "Java程序运行流程"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

#### java 如何加载的呢

1. **对于Java来说，要执行一个类的main方法，需要先加载它**。Java虚拟机规范规定，在加载之后，就要执行<cinit>方法（java代码的编译过程会把所有的静态初始化块收集到一起在字节码里创建一个<cinit>方法），所以这一点实际上是类加载的规定。main方法是一个静态方法，所以没有「类的 成员初始化 和 初始化块」发生，除非你接下来使用了new

>clinit are the static initialization blocks for the class, and static field initialization. 

2. 然后再 初始化 类中定义的方法，再执行 main()，最后才是在 heap 里分配一块内存来初始化一个对象（构造函数）—— 执行main的时候没有类的实例产生，所以没有heap内存分配和初始化方法调用发生

#### java 一个文件就是一个 class，jvm 在解析文件的时候，class 是存在哪里？

准确的说: Java的一个文件可能编译出来多个class，不过一般而言可以理解成java文件和class文件是一一对应的。class是在heap的一个特殊区域，Java8之前叫“永久代” PermGen，Java8之后叫“元空间” Metaspace，可以理解成专门存放class的地方

#### 「类」 和 「方法」 在内存中初始化和调用？

jvm 是怎么解析一个文件的，**程序执行的顺序**和在**内存分布**的情况等 —— 这其实涉及到类加载了, 请去看:《深入了解Java虚拟机》的第七章。
[深入理解Java虚拟机.pdf](https://github.com/title/tmp/blob/master/%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3Java%E8%99%9A%E6%8B%9F%E6%9C%BA%EF%BC%9AJVM%E9%AB%98%E7%BA%A7%E7%89%B9%E6%80%A7%E4%B8%8E%E6%9C%80%E4%BD%B3%E5%AE%9E%E8%B7%B5%EF%BC%88%E7%AC%AC%E4%BA%8C%E7%89%88%EF%BC%89.pdf)

* 最最简单的理解是：
  * 当一个类被加载的时候，它自己的空间在堆中被分配（包括static成员，所有的方法字节码包括<cinit>方法）。随后<cinit>方法被调用，所有的静态成员得到初始化。这是类加载后立刻发生的事情，发生在main之前。
  * class文件是一个高度结构化的数据，可以想像成一个JSON文件，只不过人类不可读罢了。JVM读取其中的所有信息，把它们存储在MetaSpace里（“类自己占用的空间”）
  * 当一个方法被调用的时候，JVM在当前线程的方法栈中开辟一个新的栈帧，栈帧的大小由方法的字节码所指定
  * 然后JVM就按照方法字节码指定的指令进行操作


* 试一试：
  ```javap -v -private XXXX.class```，它会告诉你类文件的结构。想用图形界面的话，这哥们写了个很有用的工具：[https://github.com/zxh0/classpy](