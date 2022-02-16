---
title: "微前端框架single Spa和qiankun"
subtitle: ""
date: 2020-07-15T15:59:16+08:00
draft: true
author: "gaozhidong"

description: "微前端"

tags: ["JavaScript",]
categories: ["其他"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
 
## 为什么需要微前端?
我们通过3W(what,why,how)的方式来讲解微前端

### What?什么是微前端?

![file](/images/qiankun.png)

微前端就是将不同的功能按照不同的维度拆分成多个子应用。通过主应用来加载这些子应用。

微前端的核心在于拆, 拆完后在合!

### 微前端架构具备以下几个核心价值：

* 技术栈无关 主框架不限制接入应用的技术栈，子应用具备完全自主权

* 独立开发、独立部署 子应用仓库独立，前后端可独立开发，部署完成后主框架自动完成同步更新

* 增量升级
  在面对各种复杂场景时，我们通常很难对一个已经存在的系统做全量的技术栈升级或重构，而微前端是一种非常好的实施渐进式重构的手段和策略

* 独立运行时 每个子应用之间状态隔离，运行时状态不共享

### Why?为什么去使用他?
* 不同团队间开发同一个应用技术栈不同怎么破？

* 希望每个团队都可以独立开发，独立部署怎么破？

* 项目中还需要老的应用代码怎么破？

我们是不是可以将一个应用划分成若干个子应用，将子应用打包成一个个的lib。当路径切换时加载不同的子应用。这样每个子应用都是独立的，技术栈也不用做限制了！从而解决了前端协同开发问题

怎样落地微前端?

2018年 Single-SPA诞生了， single-spa是一个用于前端微服务化的JavaScript前端解决方案 (本身没有处理样式隔离，js执行隔离) 实现了路由劫持和应用加载；

2019年 qiankun基于Single-SPA, 提供了更加开箱即用的 API （single-spa + sandbox + import-html-entry） 做到了，技术栈无关、并且接入简单（像iframe一样简单）；

总结：子应用可以独立构建，运行时动态加载主子应用完全解耦，技术栈无关，靠的是协议接入（子应用必须导出 bootstrap、mount、unmount方法）

大家肯定会问的问题：

这不是iframe吗？

如果使用iframe，iframe中的子应用切换路由时用户刷新页面会丢失当前的页面内容，回到初始话的路由页面，用户体验不好；如果是子应用嵌入到iframe里，刷新页面时，刷的是父应用的路由，此时子页面会丢失。

### 应用通信方式:

* 基于URL来进行数据传递，但是传递消息能力弱

* 基于CustomEvent实现通信 customEvent

* 基于props主子应用间通信

* 使用全局变量、Redux进行通信

### 实现微前端有哪些方案
单纯根据对概念的理解，很容易想到实现微前端的重要思想就是将应用进行拆解和整合，通常是一个父应用加上一些子应用，那么使用类似Nginx配置不同应用的转发，或是采用iframe来将多个应用整合到一起等等这些其实都属于微前端的实现方案，他们之间的对比如下：

| 方案 | 描述 | 优点 | 缺点 |
| :-----:| :----: | :----: | :----: |
| Nginx 路由转发 | 过 Nginx 配置反向代理来实现不同路径映射到不同应用 | 简单，快速，易配置 | 在切换应用时会触发浏览器刷新，影响体验 |
| iframe嵌套 | 父应用单独是一个页面，每个子应用嵌套一个iframe，父子通信可采用postMessage或者contentWindow方式	 | 实现简单，子应用之间自带沙箱，天然隔离，互不影响	 | iframe的样式显示、兼容性等都具有局限性；太过简单而显得low;刷新丢失当前子应用内容 |
| Web Components	 | 每个子应用需要采用纯Web Components技术编写组件，是一套全新的开发模式	 | 每个子应用拥有独立的script和css，也可单独部署	 | 对于历史系统改造成本高，子应用通信较为复杂易踩坑 |
| 组合式应用路由分发	 | 每个子应用独立构建和部署，运行时由父应用来进行路由管理，应用加载，启动，卸载，以及通信机制	 | 纯前端改造，体验良好，可无感知切换，子应用相互隔离 | 需要设计和开发，由于父子应用处于同一页面运行，需要解决子应用的样式冲突，变量对象污染，通信机制等技术点 |

### single-spa
在一个 single-spa 页面，注册的应用会经过下载(loaded)、初始化(initialized)、被挂载(mounted)、卸载(unmounted)和unloaded（被移除）等过程。single-spa会通过“生命周期”为这些过程提供钩子函数;

注:

* bootstrap, mount, and unmount的实现是必须的，unload则是可选的

* 生命周期函数必须有返回值，可以是Promise或者async函数

* 如果导出的是函数数组而不是单个函数，这些函数会被依次调用，对于promise函数，会等到resolve之后再调用下一个函数

* 如果 single-spa 未启动，各个应用会被下载，但不会被初始化、挂载或卸载。

#### 传参 

生命周期函数使用"props" 传参，这个对象包含single-spa相关信息和其他的自定义属性；
```
function bootstrap(props) {
 const {
   name,       // 应用名称
   singleSpa,   // singleSpa实例
   mountParcel, // 手动挂载的函数
   customProps // 自定义属性
 } = props;     // Props 会传给每个生命周期函数
 return Promise.resolve();
}
```
#### 内置参数

每个生命周期函数的入参都会保证有如下参数：

* name: 注册到 single-spa 的应用名称

* singleSpa: 对singleSpa 实例的引用, 方便各应用和类库调用singleSpa提供的API时不再导入它。 可以解决有多个webpack配置文件构建时无法保证只引用一个singleSpa实例的问题。

* mountParcel: mountParcel 函数.

#### 自定义参数 
```
// 父应用
singleSpa.registerApplication({
 name: 'app1',
 activeWhen: ['/myApp', (location) => location.pathname.startsWith('/some/other/path')],
 app,
 customProps: { authToken: "d83jD63UdZ6RS6f70D0" }
});
singleSpa.registerApplication({
 name: 'app1',
 activeWhen: ['/myApp', (location) => location.pathname.startsWith('/some/other/path')],
 app,
 customProps: (name, location) => {
   return { authToken: "d83jD63UdZ6RS6f70D0" };
 }
});
// 子应用
export function mount(props) {
 console.log(props.authToken); // 可以在 app1 中获取到authToken参数
 return vueLifecycles.mount(props);
}
```
可能使用到的场景：

* 各个应用共享一个公共的 access token

* 下发初始化信息，如渲染目标

* 传递对事件总线（event bus）的引用，方便各应用之间进行通信

注意如果没有提供自定义参数，则props.customProps默认会返回一个空对象

### qiankun
qiankun 是一个基于 single-spa 的微前端实现库，旨在帮助大家能更简单、无痛的构建一个生产可用微前端架构系统。

#### 主应用搭建
选择用vue-cli初始化了主应用，不了解的可自行阅读官方文档 项目中引入[qiankun](https://qiankun.umijs.org/zh/guide/getting-started)：

安装 

```$ yarn add qiankun # 或者 npm i qiankun -S```
在主应用中注册微应用
```
//micro/app.js
import shareData from "./shared";
/*
 * name: 微应用名称 - 具有唯一性
 * entry: 微应用入口 - 通过该地址加载微应用
 * container: 微应用挂载节点 - 微应用加载完成后将挂载在该节点上
 * activeRule: 微应用触发的路由规则 - 触发路由规则后将加载该微应用
 */
const apps = [
  {
    name: "vueApp", // 应用的名字
    entry: "//localhost:10000", // 默认会加载这个html 解析里面的js 动态的执行 （子应用必须支持跨域）fetch
    container: "#app-qiankun", // 容器名
    activeRule: "/vue", // 激活的路径
    props: { appData: shareData, data: "父应用数据111" },
  },
  {
    name: "reactApp",
    entry: "//localhost:20000", // 默认会加载这个html 解析里面的js 动态的执行 （子应用必须支持跨域）fetch
    container: "#app-qiankun",
    activeRule: "/react",//location => location.pathname.startsWith('/react')
    props: { appData: shareData, data: "父应用数据222" },
  },
];
export default apps;
//main/index.js
import { registerMicroApps, start } from 'qiankun';
import apps from './micro/app';
registerMicroApps(apps);
// 启动微应用
start();
```
> 当微应用信息注册完之后，一旦浏览器的 url 发生变化，便会自动触发 qiankun 的匹配逻辑，所有 activeRule 规则匹配上的微应用就会被插入到指定的 container 中，同时依次调用微应用暴露出的生命周期钩子。

#### 配置子应用
微应用不需要额外安装任何其他依赖即可接入 qiankun 主应用。

在主应用配置好注册的微应用后，我们需要对子应用进行配置，让子应用能接入到主应用中。

##### 子应用说明

1. 导出相应的生命周期钩子
微应用需要在自己的入口 js (通常就是你配置的 webpack 的 entry js) 导出 bootstrap、mount、unmount 三个生命周期钩子，以供主应用在适当的时机调用。
```
/**
 * bootstrap 只会在微应用初始化的时候调用一次，下次微应用重新进入时会直接调用 mount 钩子，不会再重复触发 bootstrap。
 * 通常我们可以在这里做一些全局变量的初始化，比如不会在 unmount 阶段被销毁的应用级别的缓存等。
 */
export async function bootstrap() {
  console.log('react app bootstraped');
}
/**
 * 应用每次进入都会调用 mount 方法，通常我们在这里触发应用的渲染方法
 */

export async function mount(props) {
  console.log(props);
  ReactDOM.render(<App />, document.getElementById('react15Root'));
}

/**
 * 应用每次 切出/卸载 会调用的方法，通常在这里我们会卸载微应用的应用实例
 */
export async function unmount() {
  ReactDOM.unmountComponentAtNode(document.getElementById('react15Root'));
}
/**
 * 可选生命周期钩子，仅使用 loadMicroApp 方式加载微应用时生效
 */
export async function update(props) {
  console.log('update props', props);
}
```
### 注意点 

#### 1.为什么微应用加载的资源会 404？

原因是 webpack 加载资源时未使用正确的 publicPath,两种解决方式：

a. 使用 webpack 运行时 publicPath 配置
qiankun 将会在微应用 bootstrap 之前注入一个运行时的 publicPath 变量，你需要做的是在微应用的 entry js 的顶部添加如下代码：
```
if (window.__POWERED_BY_QIANKUN__) {
  // 动态添加publicPath
  __webpack_public_path__ = window.__INJECTED_PUBLIC_PATH_BY_QIANKUN__;
}
 ```
b.使用 webpack 静态 publicPath 配置 

关于运行时 publicPath 的技术细节，可以参考 webpack 文档
```
// webpack.config.js
{
  output: {
  publicPath: `//localhost:${port}`,
}
}
```
#### 2.如何独立运行微应用

有些时候我们希望直接启动微应用从而更方便的开发调试，你可以使用这个全局变量来区分当前是否运行在 qiankun 的主应用的上下文中：
```
if (!window.__POWERED_BY_QIANKUN__) {
  render();
}
```
#### 3.配置微应用的打包工具

除了代码中暴露出相应的生命周期钩子之外，为了让主应用能正确识别微应用暴露出来的一些信息，微应用的打包工具需要增加如下配置：
```
const packageName = require('./package.json').name;
 
module.exports = {
  output: {
    // 微应用的包名，这里与主应用中注册的微应用名称一致
    library: `${packageName}-[name]`,
    // 将你的 library 暴露为所有的模块定义下都可运行的方式,其实就是将 这个类库挂载到全局的window上
    libraryTarget: 'umd',
    // 按需加载相关，设置为 webpackJsonp_vue-project 即可
    jsonpFunction: `webpackJsonp_${packageName}`,
 },
};
```

 

 

 

 