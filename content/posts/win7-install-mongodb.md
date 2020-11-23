---
title: "Win7 安装 Mongodb"
subtitle: ""
date: 2017-09-23
draft: false
author: "gaozhidong"

description: "Win7 安装 Mongodb"

tags: ["JavaScript"]
categories: []

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
## 下载安装

```
mongodb官网下载地址：[hhttps://www.mongodb.com/download-center](https://www.mongodb.com/download-center)
直接下载.msi文件并安装到指定目录即可。我的安装路径是D:\mongodb
然后在根目录下新建一个blog文件夹，作为数据存放目录（网上的教程多命名为data，你们随意，自己知道就行）。
同时在根目录下新建一个logs文件夹，作为日志文件存放处。
现在看起来可能是这样子的：
|-D:
    |-mongodb
        |- blog
        |- logs

```

## 设置系统变量

```
这一步的目的在于可以直接在cmd控制台执行mongod命令，而不需要一路cd到\bin目录才能执行。
我的电脑--属性--高级系统设置--环境变量--系统变量，找到PATH，双击编辑，在末尾加上;D:\MongoDB，注意前面加分号，最后点击确定即可
```

## 启动mongodb

```
现在，我们可以直接cmd打开命令行，直接输入
mongod --dbpath=D:\MongoDB\blog，若输出的末尾有这一句则代表mongodb已经成功启动，端口号为27017。

我们在浏览器输入localhost:27017，页面将显示“It looks like you are trying to access MongoDB over HTTP on the native driver port.”表示启动成功。
这时候新开一个命令行窗口，就可以直接执行mongo的指令了。
```

## 更快捷的方式

```
通过以上步骤，我们解决了“一路cd”的问题，但是启动mongodb还是需要写mongod --dbpath=D:\MongoDB\blog。
我们可以把mongodb作为开机启动任务，随系统开启而开启！
打开cmd控制台，输入
mongod --dbpath=D:\mongodb\blog --logpath=D:\mongodb\logs\mongodb.log --install
这时候在\logs文件夹内就会出现一个mongodb.log文件，里面是mongodb的一些日志。

现在mongodb已经可以随系统启动了。以后我们需要连接mongodb数据库，只需要在cmd控制台输入net start mongodb，

需要关闭mongodb，只需要输入net stop mongodb
```

## 下载msi 默认安装

安装mongodb服务端  示例安装目录：C:\Program Files\MongoDB

#### 用管理员打开命令行：

```
Win+R-->cmd
```

####  创建mongodb数据库和日志文件目录（自定在c盘下创建data文件夹）

```
mkdir c:\data\db
mkdir c:\data\log
```

#### 创建配置文件（日志配置、数据库配置）

```
echo logpath=c:\data\log\mongod.log> "C:\Program Files\MongoDB\Server\3.0\bin\mongod.cfg"

echo dbpath=c:\data\db>> "C:\Program Files\MongoDB\Server\3.0\bin\mongod.cfg"
```

#### 创建mongodb服务（创建后自动生成服务  services.msc）

```
sc.exe create MongoDB binPath= "\"C:\Program Files\MongoDB\Server\3.0\bin\mongod.exe\" --service --config=\"C:\Program Files\MongoDB\Server\3.0\bin\mongod.cfg\"" DisplayName= "MongoDB" start= "auto"
```

#### 启动mongodb服务

```
net start MongoDB
```

