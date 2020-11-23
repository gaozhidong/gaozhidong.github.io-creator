---
title: "Ubuntu16 配置Java环境"
subtitle: ""
date: 2017-10-06
draft: false
author: "gaozhidong"

description: "Ubuntu配置Java环境"

tags: ["Java"]
categories: []

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

## 添加源

1. 添加ppa

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
```

2. 安装oracle-java-installer

```
sudo apt-get install oracle-java8-installer
```

3. 设置系统默认jdk

```
sudo update-java-alternatives -s java-8-oracle
```

1. [官网下载](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)JDK文件jdk-8u171-linux-x64.tar.gz
2. 创建一个目录作为JDK的安装目录

```
sudo mkdir /java   
```

3. 把下载的文件移入/java目录下

```
cd 下载地址目录
sudo mv jdk-8u171-linux-x64.tar.gz /java
```

4. 解压文件

```
sudo tar -zxvf jdk-8u171-linux-x64.tar.gz
```

5. 配置环境变量

```
sudo gedit /etc/environment
在末尾加入JAVA_HOME的路径，即：
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:$JAVA_HOME/bin"
CLASSPATH=.:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
JAVA_HOME=/java/jdk1.8.0_171
```

保存退出后在运行

```
source /etc/environment //使环境变量立即生效 或者重启命令行
```

6.  测试

```
▶ java -version
openjdk version "1.8.0_171"
OpenJDK Runtime Environment (build 1.8.0_171-8u171-b11-2-b11)
OpenJDK 64-Bit Server VM (build 25.171-b11, mixed mode)

~                                                                                                                      
▶ javac -version
javac 1.8.0_171

```


