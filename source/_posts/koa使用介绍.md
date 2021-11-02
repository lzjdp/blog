---
title: koa使用介绍
date: 2021-10-29 14:27:04
tags:
---
1. koa简介
   Koa 是一个新的 web 框架，通过利用 async 函数，Koa 帮你丢弃回调函数，并有力地增强错误处理

2. 安装

```
npm install koa
```

3. Hello World

```
const Koa = require('koa')
const app = new Koa()

app.use(async ctx => {
    ctx.body = 'Hello World'
})

app.listen(3000)
```

4. Context（上下文）

Koa Context将node的request和response对象封装到单个对象中，为编写Web应用程序和API提供了许多有用的方法
```
app.use(async ctx => {
    ctx // context
    ctx.request // koa request
    ctx.response    // koa response
})
```

5. Request

request.header  请求头对象

response.method 请求方法

6. Response