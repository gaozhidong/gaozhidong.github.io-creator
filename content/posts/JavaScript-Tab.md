---
title: "HTML + JS 的一个 Tab切换"
subtitle: ""
date: 2017-03-09T08:54:35+08:00
draft: false
author: "gaozhidong"
authorLink: ""
description: ""

tags: ["JavaScript", "HTML"]
categories: ["HTML"]


featuredImage: ""
featuredImagePreview: ""

toc:
  enable: true



---

**使用原生JavaScript完成一个Tab切换**

<!--more-->

## 代码结构

### html 
```
<div class="tab">
  <ul class="tab-header clearfix">
    <li class="active">选项1</li>
    <li>选项2</li>
    <li>选项3</li>
  </ul>
  <ul class="tab-container">
    <li class="active">内容1</li>
    <li>内容2</li>
    <li>内容3</li>
  </ul>
</div>

<div class="tab">
  <ul class="tab-header clearfix">
    <li class="active">选项1</li>
    <li>选项2</li>
    <li>选项3</li>
    <li>选项4</li>
  </ul>
  <ul class="tab-container">
    <li class="active">内容1</li>
    <li>内容2</li>
    <li>内容3</li>
    <li>内容4</li>
  </ul>
</div>

<div class="tab">
  <ul class="tab-header clearfix">
    <li class="active">选项1</li>
    <li>选项2</li>
    <li>选项3</li>
    <li>选项4</li>
  </ul>
  <ul class="tab-container">
    <li class="active">内容1</li>
    <li>内容2</li>
    <li>内容3</li>
    <li>内容4</li>
  </ul>
</div>

```

### css 
``` 
ul,
li {
    margin: 0;
    padding: 0;
}

li {
    list-style: none;
}

.clearfix:after {
    content: '';
    display: block;
    clear: both;
}

.tab {
    width: 600px;
    margin: 20px auto;
    border: 1px solid #ccc;
    padding: 20px 10px;
    border-radius: 4px;
}

.tab-header {
    border-bottom: 1px solid #ccc;
}

.tab-header>li {
    float: left;
    color: brown;
    border-top: 1px solid #fff;
    border-left: 1px solid #fff;
    border-right: 1px solid #fff;
    padding: 10px 20px;
    cursor: pointer;
}

.tab-header .active {
    border: 1px solid #ccc;
    border-bottom-color: #fff;
    border-radius: 4px 4px 0 0;
    color: #333;
    margin-bottom: -1px;
}

.tab-container {
    padding: 20px 10px;
}

.tab-container>li {
    display: none;
}

.tab-container>.active {
    display: block;
}

.box {
    height: 1000px;
}

```
### js
```
let headerList = document.querySelectorAll('.tab-header li');
let panelList = document.querySelectorAll('.tab-container li');
//forEach的callback传入三个参数：currentValue、index、array
headerList.forEach(function(headerLi){
  headerLi.onclick = function(e){
    //当点击当前元素是，所有的元素去掉active
    let currentLi = e.target;
    headerList.forEach(function(li){
        li.classList.remove('active');
    })
    //当前的元素加上active类,由于headerList是类数组对象所以需要call数组方法indexOf
    let index = [].indexOf.call(headerList,currentLi);
    headerList[index].classList.add('active');
    //隐藏所有panelList，并显示当前panel
    panelList.forEach(function(panel){
        panel.classList.remove('active');
    })
    panelList[index].classList.add('active');
  }
})
```

### jQuery

```
 $('.tab-header>li').on('click',function(){
  let $this = $(this);
  $panels = $this.parents('.tab').find('.tab-container>li'),
  index = $(this).index();
  $this.siblings().removeClass('active');
  $this.addClass('active');
  $panels.removeClass('active');
  $panels.eq(index).addClass('active');
})
```

### 封装

```
function Tab(ct) {
  this.ct = ct;
  this.init();
  this.bind();
}
Tab.prototype.init = function () {
  this.headerList = this.ct.querySelectorAll('.tab-header>li');
  this.panelList = this.ct.querySelectorAll('.tab-container>li');
}
Tab.prototype.bind = function () {
  let _this = this; //把this暂存起来
  this.headerList.forEach(function (headerLi) {
    headerLi.onclick = function (e) {
      let currentLi = e.target;
      _this.headerList.forEach(function (li) {
          li.classList.remove('active');
      })
      let index = [].indexOf.call(_this.headerList, currentLi);
      _this.headerList[index].classList.add('active');
      _this.panelList.forEach(function (panel) {
          panel.classList.remove('active');
      })
      _this.panelList[index].classList.add('active');
    }
  })
}

let tab1 = new Tab(document.querySelectorAll('.tab')[0]);
let tab2 = new Tab(document.querySelectorAll('.tab')[1]);
let tab3 = new Tab(document.querySelectorAll('.tab')[2]);
//当创建了对象之后就会创建一个空对象，然后把这个对象的_proto_属性指向Tab.protitype。然后再将
//执行构造函数里的this初始化。

```