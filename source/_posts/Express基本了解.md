---
title: Express基本了解
date: 2020-02-02 13:55:27
tags: 
    - Express
categories: Express
---
# Express 

- 在 Node 中，有很多 web 开发框架 Express就是其中一个
- 官方网站： http://expressjs.com/
- Express 是 快速 简单 极简的Node.js  Web框架

### 1：安装

- 在安装Express前提下，在你当前目录下 通过 `npm init -y` 命令创建一个  `package.json` 文件 
- 通过 `npm install express --save`  命令 在当前目录下安装Express

### 2： 基本模板

```javascript
// 引入模板
var express = require('express')
// 创建 app
var app = express()

app.get('/', function(req,res){
    
})

app.listen(3000, function() {
    console.log('running...')
})
```



### 3: 利用 Express 托管静态文件  .use()

 为了提供诸如图像、CSS 文件和 JavaScript 文件之类的静态文件，请使用 Express 中的 `express.static` 内置中间件函数 

#### 语法格式：express.static(root, [options])

```javascript
// 在 Express 开放资源
// 公开指定目录
// 只要这样做了，就可以直接通过 /public/xx 的方式访问 public 目录中使用的资源了

// app.use('/public/', express.static('./public/'))
// 这样可以通过 http://127.0.0.1:端口号/views/views/xxx 方式访问 views目录的文件 
// root 参数 随便命名
app.use('/views/',express.static('./views/'))
```

### 4：Express中间件

中间件就是一堆方法，可以接收客户端发来的请求、可以对请求做出响应，也可以将请求继续交给下一个中间件继续处理

#### 官方文档：http://expressjs.com/en/guide/using-middleware.html

 中间件 功能是可以访问[请求对象](http://expressjs.com/en/4x/api.html#req)（`req`），[响应对象](http://expressjs.com/en/4x/api.html#res)（`res`）和应用程序的请求-响应周期中的下一个中间件功能的功能。下一个中间件功能通常由名为的变量表示`next` 

#### 中间件执行的规则：

认情况下，请求从上到下依次匹配中间件，一旦匹配成功，终止匹配。
可以调用next方法将请求的控制权交给下一个中间件，直到遇到结束请求的中间件。

#### 中间件的类型：

##### 应用层中间件

```javascript
// 没有请求条件的 中间件 无论谁都可以进
// 添加了 next()后 则可以在执行完此中间件后 继续 向下匹配另一个中间件
app.use(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})

// 添加了请求条件的 中间件 当请求路径匹配则进此中间件
// 显示了/user/:id路径上安装的中间件功能。该函数针对/user/:id路径上的任何类型的HTTP请求执行
app.use('/user/:id', function (req, res, next) {
  console.log('Request Type:', req.method)
  next()
})
```

##### 路由器中间件

 **路由器级中间件与应用程序级中间件的工作方式相同，只不过它绑定到的实例  `express.Router()`** 

##### 错误处理中间件

**用处**：在程序执行的过程中，不可避免的会出现一些无法预料的错误，比如文件读取失败，数据库连接失败。
错误处理中间件是一个集中处理错误的地方

 错误处理中间件始终采用**四个参数**。您必须提供四个参数以将其标识为错误处理中间件函数。即使不需要使用该`next`对象，也必须指定它以维护签名。否则，该`next`对象将被解释为常规中间件，并且将无法处理错误。 

```javascript
app.use((err, req, res, next) => {
     res.status(500).send('服务器发生未知错误');
 })
// err 就是那个错误对象

// 当程序出现错误时，调用next()方法，并且将错误信息通过参数的形式传递给next()方法，即可触发错误处理中间件
 app.get("/", (req, res, next) => {
     fs.readFile("/file-does-not-exist", (err, data) => {
         if (err) {
            next(err);  //  即可触发错误处理的中间件
         }
     });
});

```

##### 内置中间件

##### 第三方中间件

#### 中间件的一些应用之处：

**1：路由保护，客户端在访问需要登录的页面时，可以先使用中间件判断用户登录状态，用户如果未登录，则拦截请求，直接响应，禁止用户进入需要登录的页面。**

**2：网站维护公告，在所有路由的最上面定义接收所有请求的中间件，直接为客户端做出响应，网站正在维护中。**

**3：自定义404页面**









