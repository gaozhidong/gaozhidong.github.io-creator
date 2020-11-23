---
title: "WebRTC简介"
subtitle: ""
date: 2019-10-02
draft: false
author: "gaozhidong"

description: "WebRTC简介"

tags: ["WebRTC"]
categories: ["WebRTC"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
MDN上对WebRTC是这样说的：

> WebRTC (Web Real-Time Communications) 是一项实时通讯技术，它允许网络应用或者站点，在不借助中间媒介的情况下，建立浏览器之间点对点（Peer-to-Peer）的连接，实现视频流和（或）音频流或者其他任意数据的传输。WebRTC包含的这些标准使用户在无需安装任何插件或者第三方的软件的情况下，创建点对点（Peer-to-Peer）的数据分享和电话会议成为可能。

##### WebRTC的前世今生

* on2：主流的桌面及移动应用和设备 提供高质量视频压缩技术 主要视频编解码格式包括 VP3-VP8，被谷歌收购，集成到WebRTC中
* Global IP Solutions (GIPS) 的前身为Global IP Sound (GIPS)，专为数据包网络的实时通信应用市场，开发行业领先的嵌入式媒体处理解决方案。
* Google 11年收购了它们，开源了 WebRTC项目，推进标准化
* 2017年11月W3C发布了WebTTC 1.0


##### webRTC体系架构

![webRTC](/images/image-webrtc.png)
这张图来源于webRTC入门，应该每个人最开始接触webRTC时都会知道架构图，它描述了RTCPeerConnection的作用。

图中可以看出一共三个不同的层：

* web开发人员的API：包括RTCPeerConnection、RTCDataChannel和 MediaStrean对象
* 浏览器厂商的API
* 供浏览器厂商以hook方式复写的API

传输组件允许在不同类型的网络中建立连接，而语音视频引擎是负责将音频视频流从声卡和摄像机传输到网络的框架。对于web开发人员来说,最重要的部分是WebRTC API。


### 参考链接

* [Getting Started with WebRTC - HTML5 Rocks](https://www.html5rocks.com/en/tutorials/webrtc/basics/#toc-rtcpeerconnection)
