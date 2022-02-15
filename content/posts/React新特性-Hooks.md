---
title: "React新特性 Hooks"
subtitle: ""
date: 2020-06-15T15:40:29+08:00
draft: true
author: "gaozhidong"

description: "React Hooks"

tags: ["JavaScript", "React"]
categories: ["React"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。

要启用 Hook，所有 React 相关的 package 都必须升级到 16.8.0 或更高版本。

## 1. 好处
纯函数组件使用react特性
逻辑更清晰 (useEffect)
组件复用 (自定义Hooks)
## 2. 常用Hooks
```
基础 Hooks：useState，useEffect，useContext

其他 Hooks：useReducer，useCallback，useMemo，useRef，useLayoutEffect，useImperativeHandle，useDebugValue
```
### useState
跳过 state 更新：调用 State Hook 的更新函数并传入当前的 state 时，React 将跳过子组件的渲染及 effect 的执行。React使用Object.js()对比state是否更新；
把所有 state 都放在同一个 useState 调用中，或是每一个字段都对应一个 useState 调用，这两方式都能跑通。当你在这两个极端之间找到平衡，然后把相关 state 组合到几个独立的 state 变量时，组件就会更加的可读。 如果 state 的逻辑开始变得复杂，我们推荐 用 reducer 来管理它，或使用自定义 Hook。

### useEffect
副作用

数据获取，设置订阅以及手动更改 React 组件中的 DOM 都属于副作用。

分为 需要清除的 和 不需要清除 的。

* 不需要清除的：比如发送网络请求，手动变更 DOM，记录日志，这些都是常见的无需清除的操作。因为我们在执行完这些操作之后，就可以忽略他们了。

* 需要清除的：订阅外部数据源，防止内存泄露。

可以看做是componentDidMount，componentDidUpdate 和 componentWillUnmount 这三个函数的组合。 在执行 DOM 更新之后延迟调用。 清除：在 effect 返回一个函数，React 将会在组件卸载的时候调用它，执行清除操作。effect 的清除阶段在每次重新渲染时都会执行，而不是只在卸载组件的时候执行一次。

* 依赖列表中有函数，解决方案：

将函数移动到effect内部
将函数移动到组件之外
在 effect 之外调用该函数，并让 effect 依赖于它的返回值（如果你所调用的方法是一个纯计算，并且可以在渲染时调用）
万不得已，将函数加入 effect 的依赖，但 把它的定义包裹 进 useCallback Hook
effect 的依赖频繁变化，解决方案：

setState 的函数式更新形式
useReducer 把 state 更新逻辑移到 effect 之外
useRef 保存一个变量，然后对它进行读写

### useLayoutEffect
在浏览器完成布局与绘制之后，会在新一次的渲染之前，延迟调用useEffect。 然而，并非所有 effect 都可以被延迟执行。例如，在浏览器执行下一次绘制前，用户可见的 DOM 变更就必须同步执行，这样用户才不会感觉到视觉上的不一致。（概念上类似于被动监听事件和主动监听事件的区别。） useLayoutEffect会在DOM更新之后，浏览器执行绘制之前，同步调用effect，读取 DOM 布局并同步触发重渲染。

useContext
接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值。 当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定。 子组件在 context 值变化时重新渲染。

### useReducer
useState 的进阶版。 使用useReducer替代useState的情况：

state 逻辑较复杂且包含多个子值
下一个 state 依赖于之前的 state
给会触发深更新的组件做性能优化，因为你可以向子组件传递 dispatch 而不是回调函数 。

### useCallback
返回一个 memoized 回调函数。useCallback(fn, deps) 相当于 useMemo(() => fn, deps)。 当回调函数作为依赖传递给其他Hooks函数（useEffect）时使用。

### useMemo
通过记住上一次计算结果的方式在多次渲染的之间缓存计算结果，返回一个 memoized 值。 传给 useMemo 的函数是在渲染期间运行的。（依赖值改变时运行） 用处：

缓存复杂的计算结果；
跳过子节点的昂贵的重新渲染；
memoized是一种优化技术，主要用于通过存储昂贵的函数调用的结果，并在再次出现相同的输入时，返回缓存的结果，用以加速计算机程序。

 

### useRef
useRef 返回一个可变的 ref 对象，其 .current 属性被初始化为传入的参数（initialValue）。 返回的 ref 对象在组件的整个生命周期内保持不变。 当 ref 对象内容发生变化时，即变更 .current 属性不会引发组件重新渲染。如果想要在 React 绑定或解绑 DOM 节点的 ref 时运行某些代码，则需要使用回调 ref 来实现。 使用：
获取元素
保存任何可变值，其类似于在 class 中使用实例字段的方式
使用一个可变的 ref 手动存储一个布尔值来表示是首次渲染还是后续渲染，然后在你的 effect 中检查这个标识

## Hook注意事项
###  使用规则
只能在函数最外层调用 Hook。不要在循环、条件判断或者子函数中调用（Hook 在每次渲染时都按照相同的顺序被调用）
只能在 React 的函数组件或自定义Hooks中调用 Hooks。
### 自定义Hooks
自定义 Hook 是一个函数，其名称以 “use” 开头，函数内部可以调用其他的 Hook。

### 其他
React 使用 Object.is 比较算法 来比较 state。Object.is对数组和对象等引用类型的比较是通过对数组和对象的引用地址的比较实现的，若地址不变，只有内容改变，则认为该数组或对象没有改变。

　　Object.is()用于确定两个值是否相同，两个值相同有如下的几种情况：

都是 undefined
都是 null
都是 true 或 false
是长度相同的两个字符串，并且每个序号对应的字符相同
相同的两个对象（两个对象有相同的引用地址）
两个相同的数字：
都是 +0
都是 -0
都是 NaN
都不是0且不是NaN，并且值相同
Object.is与 ==运算符得到的结果不一样。==会在比较之前对符号两边的值进行强制类型转换（当他们类型不同时）。

Object.is与 ===运算符得到的结果也不一样。- 0 === + 0 是 true，而Number.NaN === NaN 是 false。

 

* Hook 能否覆盖 class 的所有使用场景？ 目前暂时还没有对应不常用的 getSnapshotBeforeUpdate，getDerivedStateFromError 和 componentDidCatch 生命周期的 Hook 等价写法。

* useCallback，useEffect，useMemo等需要依赖值的hooks，不能在hooks函数里面改变依赖值，否则hooks会无限循环。

###  问题
* useMemo 与 useCallBack的区别？

useCallback(fn, deps) 相当于 useMemo(() => fn, deps)

useMemo返回的是函数运行的结果，useCallback返回的是函数

> 官方建议：
> 你可以把 useMemo作为性能优化的手段，但不要把它当成语义上的保证。将来，React 可能会选择“遗忘”以前的一些 memoized 值，并在下次渲染时重新计算它们，比如为离屏组件释放内存。先编写在没有 useMemo 的情况下也可以执行的代码 —— 之后再在你的代码中添加 useMemo，以达到优化性能的目的。

 

### useMemo和Memo的区别？

memo针对一个组件的渲染是否重复执行

usememo针对一段函数逻辑是否重复执行

当useMemo用于记住组件渲染结果时，与Memo效果一样。

区别：

useMemo用于使 component 的部分不要进行 re-render，而不是整个 component 不要 re-render。
React.memo(component, compare)，第二个参数compare(prevProps, nextProps)用于比较props是否变化，如果第二个参数不传递，则默认只会进行 props 的浅比较。

#### useRef保存变量与useState的区别？

useRef改变时不会触发re-render