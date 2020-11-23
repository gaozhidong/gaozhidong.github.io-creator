---
title: "前端性能优化"
subtitle: ""
date: 2019-07-23
draft: false
author: "gaozhidong"

description: "前端性能优化"

tags: ["JavaScript", "HTML"]
categories: ["HTML"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

### 网络层面

#### 请求过程的优化

##### HTTP请求优化

* Gzip压缩

```
//request headers 中加上这么一句
accept-encoding:gzip
```

* 图片优化
  **WebP**是 Google 专为 Web 开发的一种旨在加快图片加载速度的图片格式，它支持有损压缩和无损压缩。

#### 减少网络请求

* 浏览器缓存
  浏览器缓存机制有四个方面，它们按照获取资源时请求的优先级依次排列如下：

* Memory Cache
* Service Worker Cache
* HTTP Cache
* Push Cache


### 渲染层面

#### 服务端渲染

* 服务端渲染通常是为了SEO，但是服务端渲染解决了一个非常关键的性能问题——首屏加载速度过慢。


#### 浏览器的渲染机制

* CSS性能方案
* JS性能方案

#### DOM优化

* 原理和思路
* 异步循环与异步更新
* 回流与重绘

#### 首屏渲染

* 懒加载


### 性能监控

#### 可视化工具

* [Peformance](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/reference)
  Performance 是 Chrome 提供给我们的开发者工具，用于记录和分析我们的应用在运行时的所有活动。它呈现的数据具有实时性、多维度的特点，可以帮助我们很好地定位性能问题。

* [LightHouse](https://developers.google.com/web/tools/lighthouse/?hl=zh-cn)

>Lighthouse 是一个开源的自动化工具，用于改进网络应用的质量。 你可以将其作为一个 Chrome 扩展程序运行，或从命令行运行。 为Lighthouse 提供一个需要审查的网址，它将针对此页面运行一连串的测试，然后生成一个有关页面性能的报告。 


#### W3C性能API

W3C 规范为我们提供了 [Performance](https://developer.mozilla.org/zh-CN/docs/Web/API/Performance) 相关的接口。它允许我们获取到用户访问一个页面的每个阶段的精确时间，从而对性能进行分析。我们可以将其理解为 Performance 面板的进一步细化与可编程化。
**访问 performance 对象**performance 是一个全局对象。 window.performance