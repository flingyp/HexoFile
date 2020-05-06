---
title: 服务端中get和post获取数据的方法
date: 2020-02-02 19:26:39
tags: 
    - NodeJS
categories: Node.js
---
## get 获取请求数据

**`req.query`  （获取 get 请求数据）**

```javascript
// req.query 用于获取 request 的请求内容

// GET /search?q=tobi+ferret
console.dir(req.query.q)
// => 'tobi ferret'

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
console.dir(req.query.order)
// => 'desc'

console.dir(req.query.shoe.color)
// => 'blue'

console.dir(req.query.shoe.type)
// => 'converse'

// GET /shoes?color[]=blue&color[]=black&color[]=red
console.dir(req.query.color)
// => ['blue', 'black', 'red']
```

## POST 获取请求数据

**（在Express 获取 POST 请求数据 (req.body)）**

**在Express 中没有内置获取表单 POST 请求的API，这里想要使用一个第三方插件： `body-parser`**

#### 1： 安装

```shell
npm install --save body-parser
```

#### 2： 配置

```javascript
var express = require('express')
// 引包 安装后 引入body-parser
var bodyParser = require('body-parser')

var app = express()

   	 // 配置部分	这一部分不用动
// 配置 body-parser
// 只要加入这个配置，则在 req 请求对象上会多出来一个属性： body
// 也就是说你就可以通过 req.body 来获取表单 POST 请求体数据了
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())
```

#### 3： 使用

```javascript
// 获取 POST请求数据 第一步： 先安装  
//				   第二步： 引包 var bodyParser = require('body-parser')
//				   第三步： 把 第二部分 的两条代码加上去 之后就可以获取数据了 通过 req.body的方式
```

