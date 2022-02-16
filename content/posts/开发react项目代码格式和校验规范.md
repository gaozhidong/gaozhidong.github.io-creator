---
title: "开发react项目代码格式和校验规范"
subtitle: ""
date: 2021-03-16T10:48:45+08:00
draft: true
author: "gaozhidong"

description: "React ESLint"

tags: ["JavaScript", "React","VS Code"]
categories: ["ESLint"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

前端react项目，不管是用create-react-app 初始化的，还是用阿里的 [umi](https://umijs.org/zh-CN/docs) 初始化项目，原则上开发语言都要用typescript，所以相关的eslint 和 prettier配置都要加入ts的相关检测特征。为了简化繁琐的配置，使用umi封装的@umijs/fabric 包对 eslint stylelint和prettier的初始配置做了封装，可初始化一些预设配置。<br />
<br />相关的 [文档](https://github.com/umijs/fabric)可参考<br />

<a name="oSNOG"></a>
## 配置的步骤如下：

<br />安装 @umijs/fabric、eslint、stylelint、prettier、typescript
```javascript
npm i @umijs/fabric eslint stylelint typescript prettier -D
```
<a name="yy2Xe"></a>
###  .eslintrc.js文件配置
```javascript
module.exports = {
  extends: [require.resolve('@umijs/fabric/dist/eslint')],
  // in antd-design-pro
  globals: {
    ANT_DESIGN_PRO_ONLY_DO_NOT_USE_IN_YOUR_PRODUCTION: true,
    page: true,
  },
  rules: {
    // 自定义的其他配置
  },
};
```
<a name="r3VY7"></a>
### .stylelintrc.js文件配置
```javascript
module.exports = {
  extends: [require.resolve('@umijs/fabric/dist/stylelint')],
  rules: {
    // 自定义的其他配置
  },
};
```
<a name="WNFnL"></a>
### .prettierrc.js文件配置
```javascript
const fabric = require('@umijs/fabric');
module.exports = {
  ...fabric.prettier,
};
```
<a name="nbwAb"></a>
### .editorconfig文件配置
```javascript
# http://editorconfig.org
root = true
[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
[*.md]
trim_trailing_whitespace = false
[Makefile]
indent_style = tab
```
<a name="HBAnO"></a>
### tsconfig.json文件配置
```javascript
{
  "compilerOptions": {
    "outDir": "build/dist",
    "module": "esnext",
    "target": "esnext",
    "lib": ["esnext", "dom"],
    "sourceMap": true,
    "baseUrl": ".",
    "jsx": "preserve",
    "allowSyntheticDefaultImports": true,
    "moduleResolution": "node",
    "forceConsistentCasingInFileNames": true,
    "noImplicitReturns": true,
    "suppressImplicitAnyIndexErrors": true,
    "noUnusedLocals": true,
    "allowJs": true,
    "skipLibCheck": true,
    "experimentalDecorators": true,
    "strict": true,
    "noImplicitAny": false,
    "paths": {
      "@/*": ["./src/*"],
      "@@/*": ["./src/.umi/*"]
    },
    "resolveJsonModule": true
  },
  "include": [
    "mock/**/*",
    "src/**/*",
    "tests/**/*",
    "test/**/*",
    "__test__/**/*",
    "typings/**/*",
    "config/**/*",
    ".eslintrc.js",
    ".stylelintrc.js",
    ".prettierrc.js",
    "jest.config.js",
    "mock/*"
  ],
  "exclude": ["node_modules", "build", "dist", "scripts", "src/.umi/*", "webpack", "jest"]
}
```
<a name="NJA13"></a>
### VSCODE编辑器的相关配置

<br />检查vscode中eslint和prettier插件是否正确安装（注意，eslint一定要安装正确的版本，注意作者是Dirk Baeumer)<br />
<br />[https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)<br />
<br />[https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)<br />
<br />打开vscode命令行,输入json,打开工作区设置（只针对当前项目）<br />

![file](/images/2021-1.png)

添加如下配置：
```javascript
{
  "editor.codeActionsOnSave": {
  	"source.fixAll.eslint": true
  }
}
```

<br />保存后即可生效。<br />

