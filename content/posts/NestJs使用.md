---
title: "NestJs使用"
subtitle: ""
date: 2021-02-15T16:52:34+08:00
draft: true
author: "gaozhidong"

description: "这是描述"

tags: ["JavaScript", "HTML"]
categories: ["HTML"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
 
# NestJS 
[Nest](https://nestjs.bootcss.com/)官网
> Nest (NestJS) 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的开发框架。它利用 JavaScript 的渐进增强的能力，使用并完全支持 TypeScript （仍然允许开发者使用纯 JavaScript 进行开发），并结合了 OOP （面向对象编程）、FP （函数式编程）和 FRP （函数响应式编程）。

> 在底层，Nest 构建在强大的 HTTP 服务器框架上，例如 Express （默认），并且还可以通过配置从而使用 Fastify ！

> Nest 在这些常见的 Node.js 框架 (Express/Fastify) 之上提高了一个抽象级别，但仍然向开发者直接暴露了底层框架的 API。这使得开发者可以自由地使用适用于底层平台的无数的第三方模块。



## Nest有三种基本的应用程序构建块
1. 模块 @Module({}) ，提供元数据
2. 控制器 @Controller()，处理HTTP请求
3. 组件 @Component()，几乎所有的事物都可以被看作一个组件--Service, Repository, Provider等。

### 核心文件
* app.controller.ts：单路径的简单的控制器
* app.module.ts：项目的root模块
* main.ts：项目的入口文件，创建nest应用

### 数据库
* 安装typeorm,mysql：```npm install --save @nestjs/typeorm typeorm mysql```
* 配置：ormconfig.json
* 注入：app.module.ts
* 定义实体：entities/**.entity.ts

### Controller
* 创建：nest g controller taskList
* 请求方法：@Get(), @Post(), @Put(), @Delete(), @Patch(), @Options(), @Head(), @All()
* 状态码：@HttpCode（200），@HttpCode（404）
* 自定义请求Header：@Header('Cache-Control', 'none')

### Provider
@Injectable()

* 几乎所有的东西都可以被认为是提供者 - service, repository, factory, helper 等,通过 constructor 注入依赖关系
* service：
* 创建：nest g service tasklist

### module
```
@module({
  provider`s:[] //引入并实例化的provider，并且可以至少在整个module中共享，service
  controllers:[AppController,...] //必须创建的一组controllers
  imports:[] //导入的其他模块的列表，这些模块导出了该模块中所需的provider
  exports：[] `// 本模块导出的provider，可以被其他导入该模块的文件使用
})
```

* 创建：nest g module tasklist
* 用处：组织应用程序结构
* 功能模块：每个功能模块中有一个module，组织该功能的controllers，services，components并输出，在根目录的app.module.ts中引入。

### Middleware
* 在路由处理之前被调用，用于修改请求/响应对象、周期
* 不能在@module()列出，需使用configure()设置
* 全局中间件：main.ts中app.use()

### Exception filters
* 异常过滤器：捕获 HttpException 类的实例，并为它们设置自定义响应逻辑，@Catch(HttpException)
* 使用范围：路由、controller、全局
* 捕获一切异常：自定义异常过滤器


### Pipes
* 将输入数据转换为所需的输出，可以处理验证
* @UsePipes( )，app.useGlobalPipes( )
* whitelist：白名单，过滤在dto中未定义的字段，app.useGlobalPipes({whitelist：true})
* 两个内置pipes

#### 1. validationPipe：
* @UsePipes()绑定
* 创建dto时使用typeScript验证：安装插件 $ npm i --save class-validator * class-transformer
* 可全局配置，使用时只需在dto中标明类型
#### 2. ParseIntPipe

* 将一个字符串解析为一个整数值
* 用于格式化转换前端传入的参数

### Serialization
* @Exclude()：返回数据去掉该字段，password
* @Expose()：返回数据中加入该字段，不存在在数据库中，由计算得出

### 执行顺序
客户端请求 ---> 中间件 ---> 守卫 ---> 拦截器之前 ---> 管道 ---> 控制器处理并响应 ---> 拦截器之后 ---> 过滤器



 