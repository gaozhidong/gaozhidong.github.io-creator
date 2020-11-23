---
title: "WebRTC涉及名词和学习资料"
subtitle: ""
date: 2019-10-06
draft: false
author: "gaozhidong"

description: "WebRTC涉及名词和学习资料"

tags: ["WebRTC"]
categories: ["WebRTC"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

### UDP和TCP

* [TCP和UDP的区别](https://zhuanlan.zhihu.com/p/24860273)
* [TCP和UDP的最完整的区别](https://blog.csdn.net/Li_Ning_/article/details/52117463)
* [TCP/UDP协议详解](https://juejin.im/post/5d2757356fb9a07ef7109ecc)

### RTP/RTCP

* [RTP/RTCP协议解析](https://blog.csdn.net/machh/article/details/51868569)
* [RTP/RTSP/RTCP有什么区别？](https://www.zhihu.com/question/20278635)
* [实时传输协议](https://baike.baidu.com/item/%E5%AE%9E%E6%97%B6%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE/9365206?noadapt=1&fromtitle=RTP%2FRTCP&fromid=7518582)


### SRTP/SRTCP

维基百科：安全实时传输协议

> 安全实时传输协议（Secure Real-time Transport Protocol或SRTP）是在实时传输协议（Real-time Transport Protocol或RTP）基础上所定义的一个协议，旨在为单播和多播应用程序中的实时传输协议的数据提供加密、消息认证、完整性保证和重放保护。它是由David Oran（思科）和Rolf Blom（爱立信）开发的，并最早由IETF于2004年3月作为RFC 3711发布。

> 由于实时传输协议和可以被用来控制实时传输协议的会话的实时传输控制协议（RTP Control Protocol或RTCP）有着紧密的联系，安全实时传输协议同样也有一个伴生协议，它被称为安全实时传输控制协议（Secure RTCP或SRTCP）；安全实时传输控制协议为实时传输控制协议提供类似的与安全有关的特性，就像安全实时传输协议为实时传输协议提供的那些一样。

> 在使用实时传输协议或实时传输控制协议时，使不使用安全实时传输协议或安全实时传输控制协议是可选的；但即使使用了安全实时传输协议或安全实时传输控制协议，所有它们提供的特性（如加密和认证）也都是可选的，这些特性可以被独立地使用或禁用。唯一的例外是在使用安全实时传输控制协议时，必须要用到其消息认证特性。


### [DTLS](https://baike.baidu.com/item/DTLS)

DTLS的主要用途，就是让通信双方协商密钥，用来对数据进行加解密。

1. 通信双方：通过DTLS握手，协商生成一对密钥；
2. 发送方：对数据进行加密；
3. 发送方：通过UDP传输加密数据；
4. 接收方：对加密数据进行解密；


### STUN/TURN NAT打洞  NAT穿越 P2P穿越 ICE

* [P2P技术之STUN、TURN、ICE详解](http://www.52im.net/thread-557-1-1.html)
* [WebRTC直播技术(二)-ICE/STUN/TURN](https://imweb.io/topic/5a4a6cb2a192c3b460fce37f)
* [WebRTC之STUN、TURN和ICE研究](https://www.jianshu.com/p/78ab26a73915)
  [P2P通信标准协议(一)之STUN](https://evilpan.com/2015/12/12/p2p-standard-protocol-stun/)

### 真实的SDP片段

```

// v 开始会话级描述
v=0
o=- 7017624586836067756 2 IN IP4 127.0.0.1
s=-
t=0 0
 
// m 开始媒体级描述
//下面 m= 开头的两行，是两个媒体流：一个音频，一个视频。
m=audio 9 UDP/TLS/RTP/SAVPF 111 103 104 9 0 8 106 105 13 126
...
m=video 9 UDP/TLS/RTP/SAVPF 96 97 98 99 100 101 102 122 127 121 125 107 108 109 124 120 123 119 114 115 116

```

>上面的SDP片段所示，该 SDP 中描述了一路音频流，即m=audio，该音频支持的 Payload ( 即数据负载 ) 类型包括 111、103、104等等。

>在该 SDP 片段中又进一步对 111、103、104 等 Payload 类型做了更详细的描述，如 a=rtpmap:111 opus/48000/2 表示 Payload 类型为 111 的数据是 OPUS 编码的音频数据，并且它的采样率是 48000，使用双声道。以此类推，你也就可以知道 a=rtpmap:104 ISAC/32000 的含义是音频数据使用 ISAC 编码，采样频率是 32000，使用单声道。


## webRTC脑图

![webRTC脑图](/images/image-webrtc2.png)
## 参考资料

* [WebRTC：数据传输相关协议简介](https://www.cnblogs.com/chyingp/p/11198874.html)

* [WebRTC：一个视频聊天的简单例子](https://www.cnblogs.com/chyingp/p/example-of-video-chat-using-webrtc.html)

* [免费开源项目starRTC](https://github.com/starrtc)

* [WebRTC学习](https://miaopei.github.io/2019/05/14/WebRTC/webrtc-01/)

* [WebRTC实验](https://github.com/muaz-khan/WebRTC-Experiment)

* [官方文档](http://w3c.github.io/webrtc-pc/)
