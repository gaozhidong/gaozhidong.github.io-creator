---
title: "npm 常见的一些配置"
subtitle: ""
date: 2017-08-23
draft: false
author: "gaozhidong"

description: "npm 一些配置"

tags: ["npm", "JavaScript"]
categories: ["JavaScript"]

featuredImage: ""
featuredImagePreview: ""
---
**npm 小技巧** 
<!--more-->

* 运行 ```npm config set loglevel http```， npm 发出的请求
* 运行 ```npm config set progress false```，关闭进度条
* 运行 ```npm config set registry https://registry.npm.taobao.org/```
* 这会让你在运行 npm adduser 的时候出问题，想要恢复成原样，只需要 ```npm config delete registry``` 即可
* 还原 ```npm config set registry https://registry.npmjs.org/```


## 清除缓存  

```
npm cach clean --force
```

## node-sass 安装失败

```
$ npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
```

## chromedriver_win32 下载失败

```
npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```

## npm scripts 规则

```
"scripts": {
    "lint": "eslint --fix --ext .js,.vue src",
  },
  
  
eslint --fix 可以按照eslint规则自动格式化
```

**Module build failed: Error: No parser and no file path given, couldn’t infer a parser** 的错误。


```
rm -rf node_modules
npm install
npm install prettier@~1.12.1
```


## npm 常用的包

* [nodemon](https://www.npmjs.com/package/nodemon) 

* [bcrypt](https://www.npmjs.com/package/bcrypt)

* [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)

* [http-assert](https://www.npmjs.com/package/http-assert)

* [pm2](https://www.npmjs.com/package/pm2)

