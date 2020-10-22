---
weight: 1
title: "弹窗"
date: 2017-03-06T21:40:32+08:00
draft: false
author: "gaozhidong"
description: "HTML + JS 的一个 弹窗 ."
resources:
- name: "featured-image"
  src: "featured-image.jpg"

tags: ["JavaScript", "HTML"]
categories: ["HTML"]

lightgallery: true

toc:
  auto: false
---

HTML + JS 的一个 弹窗 

<!--more-->

## HTML + JS 的一个 弹窗 

##### html 
```
<div id='one'>
  <button id='btn'>点我</button>
</div>
<div id='two'>
  <button id='btn'>不要点我</button>
</div>
<div id='three'>
  <button id='btn'>我是第三个</button>
</div>
```

##### css 
``` 
* {
  margin: 0;
  padding: 0;
}

.overlay {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.3);
  position: fixed;
  left: 0;
  top: 0;
}

.floatwin {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 350px;
  background: #FFF;
  left: 50%;
  border-radius: 4px;
}

.clear:after {
  content: '';
  display: block;
  clear: both;
}

.header {
  padding: 8px 10px;
  border-bottom: 1px solid #ccc;
}

.header>span {
  float: right;
  margin: 0;
  cursor: pointer;
}

.content {
  padding: 20px 10px;
}

.content>p {
  line-height: 1.5;
}

.footer {
  border-top: 1px solid #ddd;
  padding: 0px 10px;
}

.footer>span {
  display: inline-block;
  float: right;
  margin: 10px 0px 10px 10px;
  cursor: pointer;
}

```
##### js
```
var Modal = (function () {
			function _Modal(ct, header, content) {
  this.ct = ct
  this.header = header
  this.content = content
  this.init()
  this.bind()
}

_Modal.prototype = {
  init: function () {
    var div = this.div = document.createElement('div')
    div.innerText = '1'
    this.html = '<div class="overlay dis close">'
    this.html += '<div class="floatwin ">'
    this.html += '<div class="header clear">'
    this.html += '<span class="close">X</span>'
    this.html += '<h4>' + this.header + '</h4>'
    this.html += '</div>'
    this.html += '<div class="content">'
    this.html += '<p>' + this.content + '</p>'
    this.html += '</div>'
    this.html += '<div class="footer clear">'
    this.html += '<span>确定</span>'
    this.html += '<span class="close">取消</span></div></div></div>'
    div.innerHTML = this.html
    console.log(this.html)
  },
  bind: function () {
    var _this = this
    console.log(this.ct.querySelectorAll('.close').length)
    this.ct.querySelector('#btn').addEventListener('click', function (e) {
      e.stopPropagation();
      _this.ct.appendChild(_this.div)
    })
    for (i = 0; i < this.div.querySelectorAll('.close').length; i++) {
      console.log(1)
      this.div.querySelectorAll('.close')[i].addEventListener('click', function (e) {
        e.stopPropagation();
        console.log(1)
        _this.div.parentNode.removeChild(_this.div)
      })
    }
    this.div.querySelector('.floatwin').addEventListener('click', function (e) {
      e.stopPropagation();
    })
  }
}
return {
  add: function (ct, header, content) {
    new _Modal(ct, header, content)
  }
}
})()

Modal.add(document.querySelector('#one'), '标题啦', '内容啦')
Modal.add(document.querySelector('#two'), '标题啦2', '内容啦2')
Modal.add(document.querySelector('#three'), '标题啦3', '内容啦4')

```