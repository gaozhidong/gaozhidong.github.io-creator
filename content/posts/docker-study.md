---
title: "Docker 基本命令"
subtitle: ""
date: 2019-03-23
draft: false
author: "gaozhidong"

description: "初步学习Docker"

tags: ["Docker"]
categories: ["Docker"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

### 什么是Docker 

Docker是一个开源的应用容器引擎，提供了一种在安全、可重复的环境中自动部署软件的方式，允许开发者将他们的应用和依赖包打包到一个可移植的容器中，然后发布到任何流行的Linux机器上，也可以实现虚拟化。

Docker 在容器的基础上，进行了进一步的封装，从文件系统、网络互联到进程隔离等等，极大的简化了容器的创建和维护。使得 Docker 技术比虚拟机技术更为轻便、快捷。

### Docker基本概念

Docker 包括三个基本概念

* 镜像（Image） 一个特殊的文件系统
* 容器（Container） 镜像运行时的实体
* 仓库（Repository） 集中存放镜像文件的地方

#### Docker 安装

```
//deepin 系统
sudo apt-get install docker-ce
```

#### docker 一些命令

**Hello World**

```
docker run hello-world
```

**查看docker信息**

```
docker info
```

![image](402F513AAA3841FB881CA4C1B2148FCB)

**启动docker**

```
systemctl start docker
```

**重启docker**

```
sudo service docker restart
```

**查看容器**

```
docker ps # 查看运行中的容器
docker ps -a # 查看所有容器
```

**列出镜像**

```
docker image ls
```

**查看所有已经创建的包括终止状态的容器**

```
docker container ls -a
```

**镜像体积**

```
docker system df
```

**终止容器**

```
docker container stop
```

**删除容器**

```
docker container rm  //删除一个处于终止状态的容器
```

**清理所有处于终止状态的容器**

```
docker container prune
```

**容器操作**

```
# 停止一个容器
docker stop $JOB

# 启动一个已经创建的容器
docker start $JOB

# 重启一个容器
docker restart $JOB

# 停止一个容器
docker kill $JOB

# 删除一个容器
docker stop $JOB # 必须先停止
docker rm $JOB
```

#### 更换国内的 docker 加速器

1. 编辑 /etc/docker/daemon.json 文件，并输入 docker-cn 镜像源地址

```
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

2. 重启docker服务

```
sudo service docker restart
```

## 学习资料

* [Docker — 从入门到实践](https://github.com/yeasy/docker_practice)
* [Docker基础](https://yq.aliyun.com/articles/130)
* [从 0 开始了解 Docker](https://github.com/rccoder/blog/issues/31)

