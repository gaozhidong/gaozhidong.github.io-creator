---
title: "WebRTC核心API"
subtitle: ""
date: 2019-10-04
draft: false
author: "gaozhidong"

description: "WebRTC核心API"

tags: ["WebRTC"]
categories: ["WebRTC"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

WebRTC核心API可以分为两类

#### Streams

> Streams API允许JavaScript以编程的方式访问通过网络接收的数据流，并根据开发人员的需要处理它们。

###### MediaDevices 

MediaDevices 接口提供访问连接媒体输入的设备，如照相机和麦克风，以及屏幕共享等。

* enumerateDevices() 
  可用的媒体输入和输出设备的列表，例如麦克风，摄像头，耳机设备。切换设备时用

* getDisplayMedia()
  选择和授权捕获用户选择的屏幕区域以及一个可选的音频轨道

* getStupportedConstraints()
  监视客户端所支持的约束属性，比如视频高宽，码率等

* getUserMedia()
  提示用户授权使用媒体输入，媒体输入会产生MediaStream，里面包含了请求的媒体类型的音视频或其他轨道

如果网页使用了getUserMedia方法，浏览器就会询问用户，是否同意浏览器调用麦克风或摄像头。如果用户同意，就调用回调函数onSuccess；如果用户拒绝，就调用回调函数onError

* 成功回调函数

获取多媒体设备成功时调用。onSuccess回调函数的参数是一个数据流对象stream。stream.getAudioTracks方法和stream.getVideoTracks方法，分别返回一个数组，其成员是数据流包含的音轨和视轨（track）。

使用的声音源和摄影头的数量，决定音轨和视轨的数量。比如，如果只使用一个摄像头获取视频，且不获取音频，那么视轨的数量为1，音轨的数量为0。每个音轨和视轨，有一个kind属性，表示种类（video或者audio），和一个label属性（比如FaceTime HD Camera (Built-in)）。

* 失败回调函数

获取多媒体失败时调用。Error对象的code属性有说明错误的类型：

* PERMISSION_DENIED：用户拒绝提供信息。
* NOT_SUPPORTED_ERROR：浏览器不支持硬件设备。
* MANDATORY_UNSATISFIED_ERROR：无法发现指定的硬件设备。

```
//新版本Chrome中getUserMedia接口在http下不再支持。要使用HTTPS协议

navigator.getUserMedia = navigator.getUserMedia ||
        navigator.webkitGetUserMedia ||
        navigator.mozGetUserMedia; //兼容
		
navigator.getUserMedia({
	audio: true,
	video: {
		width: 1280,
		height: 720
	}
}, (success)=>{
	console.log('success'+ success)
	 let video = document.querySelector("video");
     // video.src = window.URL.createObjectURL(stream);这种写法已被移除
	 video.srcObject = stream;
}, (error)=>{
	console.log('err'+ error)
});
// 如果存在回声，应该在video或者audio节点处添加muted，进行简单的回声消噪
```

[demo](https://www.webrtc-experiment.com/RecordRTC/)

#### RTCPeerConnection

> RTCPeerConnection 接口代表一个由本地计算机到远端的WebRTC连接。该接口提供了创建，保持，监控，关闭连接的方法的实现。

不同客户端之间的音频/视频传递，是不用通过服务器的。但是，两个客户端之间建立联系，需要通过服务器。服务器主要转递两种数据。

>  通信内容的元数据：打开/关闭对话（session）的命令、媒体文件的元数据（编码格式、媒体类型和带宽）等。
>  网络通信的元数据：IP地址、NAT网络地址翻译和防火墙等。

```
var signalingChannel = createSignalingChannel();
var pc;
var configuration = ...;

// run start(true) to initiate a call
function start(isCaller) {
    pc = new RTCPeerConnection(configuration);

    // send any ice candidates to the other peer
    pc.onicecandidate = function (evt) {
        signalingChannel.send(JSON.stringify({ "candidate": evt.candidate }));
    };

    // once remote stream arrives, show it in the remote video element
    pc.onaddstream = function (evt) {
        remoteView.src = URL.createObjectURL(evt.stream);
    };

    // get the local stream, show it in the local video element and send it
    navigator.getUserMedia({ "audio": true, "video": true }, function (stream) {
        selfView.src = URL.createObjectURL(stream);
        pc.addStream(stream);

        if (isCaller)
            pc.createOffer(gotDescription);
        else
            pc.createAnswer(pc.remoteDescription, gotDescription);

        function gotDescription(desc) {
            pc.setLocalDescription(desc);
            signalingChannel.send(JSON.stringify({ "sdp": desc }));
        }
    });
}

signalingChannel.onmessage = function (evt) {
    if (!pc)
        start(false);

    var signal = JSON.parse(evt.data);
    if (signal.sdp)
        pc.setRemoteDescription(new RTCSessionDescription(signal.sdp));
    else
        pc.addIceCandidate(new RTCIceCandidate(signal.candidate));
};
```

RTCPeerConnection带有浏览器前缀，Chrome浏览器中为webkitRTCPeerConnection，Firefox浏览器中为mozRTCPeerConnection。Google维护一个函数库[adapter.js](https://github.com/webrtcHacks/adapter)，用来抽象掉浏览器之间的差异。

### 参考链接

* [MDN Streams API](https://developer.mozilla.org/zh-CN/docs/Web/API/Streams_API)
* [MDN MediaDevices](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices)
* [MDN RTCPeerConnection](https://developer.mozilla.org/zh-CN/docs/Web/API/RTCPeerConnection)
* [WebRTC 教程](https://www.kaifaxueyuan.com/frontend/webrtc.html)
* [WebRTC -- JavaScript 标准参考教程](https://javascript.ruanyifeng.com/htmlapi/webrtc.html#toc1)

