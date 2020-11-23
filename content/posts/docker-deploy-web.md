---
title: "Docker 部署简单的 Web 服务"
subtitle: ""
date: 2019-04-20
author: "gaozhidong"

description: "Docker 部署简单的 Web 服务"

tags: ["Docker", "Web"]
categories: ["Web"]

featuredImage: ""
featuredImagePreview: ""
---

**Docker 部署 Web**
<!--more-->
## 目录结构

首先，根据以下目录建立对应的文件。

```text
.
├ test.js
├ DockerFile
├ package.json
```

test.js 文件内容如下：

```js
const Koa = require('koa');
const app = new Koa();
app.use(function(ctx) {
  ctx.body = 'hello docker';
});
app.listen(8998);
```

DockerFile 文件内容如下：

```dockerfile
FROM node
COPY . /app
WORKDIR /app
RUN ["npm", "install"]
EXPOSE 3456
CMD node test.js
```

## 生成镜像

执行命令生成自定义镜像。

```sh
docker image build . -t mytest1
```

## 运行容器

将刚刚创建的镜像，通过容器跑起来。

```sh
docker container run -p 8000:8998 mytest1
```

执行完毕之后，在浏览器中直接访问 localhost:8000 就可以看到 hello docker 了。