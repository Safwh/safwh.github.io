---
title: node创建web服务器测试打包文件
date: 2019-12-26 21:01:50
tags:
---

## 新建一个 node 项目,并安装 express

新建一个 server 文件夹 , 在 server 目录打开控制台

```bash
$ yarn init
```

安装 express

```bash
$ yarn add express
```

## 将打包的 dist 文件夹复制到 server 文件夹中

## 新建一个入口文件 app.js

```javascript
const express = require("express");
// 创建web服务器
const app = express();

/// 托管静态资源
app.use(express.static("./dist"));

// 启动web服务器
app.listen(80, () => {
  console.log("server running at http://127.0.0.1");
});
```

## 运行 app.js

```bash
$ node .\app.js
```

## 打开 127.0.0.1 就可以看到页面
