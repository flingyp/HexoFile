---
title: Nodejs初步了解
date: 2020-02-02 19:24:18
tags: 
    - NodeJS
categories: Node.js
---

## Node.js介绍

**1、官方解释：**

Node.js 是一个基于 **Chrome V8** 引擎的 JavaScript 运行环境。 Node.js使用了一个**事件驱动**、**非阻塞式I/O**的模型（ Node.js的特性），使其轻量级又高效。 Node.js 的包管理器 npm 是全球最大的开源库生态系统。

![](http://img.smyhvae.com/20180301_1540.png)

如上图所示：

- Node 内部采用 Google Chrome 的 V8 引擎，作为 JavaScript 语言解释器；

- 通过自行开发的 libuv 库，调用操作系统资源。

**2、非官方解释：**

**Node.js**：是 JavaScript 语言在服务器端的运行环境（平台）。

**总结：**

**Node.js 是一个 JavaScript 的运行环境（平台）**，不是一门语言，也不是 JavaScript 的框架。

## Node.js的特点

**单线程**

## Node 的常用命令

查看 node 的版本：

```
$ node -v
```

执行脚本字符串：

```
$ node -e 'console.log("Hello World")'
```

运行脚本文件：

```
$ node index.js

$ node path/index.js

$ node path/index
```

查看帮助：


```
$ node --help

```

## 包和 NPM

### 什么是包


由于 Node 是一套轻内核的平台，虽然提供了一系列的内置模块，但是不足以满足开发者的需求，于是乎出现了包（package）的概念：
与核心模块类似，就是将一些预先设计好的功能或者说 API 封装到一个文件夹，提供给开发者使用。

Node 本身并没有太多的功能性 API，所以市面上涌现出大量的第三方人员开发出来的 Package。

### 包的加载机制

如果 Node中自带的包和第三方的包名冲突了，该怎么处理呢？原则是：

- 先在系统核心（优先级最高）的模块中找；

- 然后到当前项目中 node_modules 目录中找。


比如说：

```
requiere(`fs`)
```

那加载的肯定是系统的包。所以，我们尽量不要创建一些和现有的包重名的包。

### NPM的概念

>包的生态圈一旦繁荣起来，就必须有工具去来管理这些包。NPM 应运而生。

**NPM**：Node Package Manager。官方链接： <https://www.npmjs.com/>

随着时间的发展，NPM 出现了两层概念：

- 一层含义是 Node 的开放式模块登记和管理系统，亦可以说是一个生态圈，一个社区。

- 另一层含义是 Node 默认的模块管理器，是一个命令行下的软件，用来安装和管理 Node 模块。

## NPM不需要单独安装

NPM 不需要单独安装。默认在安装 Node 的时候，会连带一起安装 NPM

## npm常用命令

###  npm 命令行工具

- npm 的第二层含义就是一个命令行工具，只要安装了 node 就已经安装了 npm

- npm也有版本的概念

  - 可以通过在命令行输入：

  - ```
    npm --version   //查看版本号
    ```

- 升级 npm （无所谓）

  - ```
    npm install --global npm
    ```

### 常用命令

- npm init
  - npm init -y  可以跳过向导，快速生成
- npm install 
  - 一次性安装 dependencies 选项中依赖项全部安装
- npm install 包名 (简写： npm i 包名)
  - 只下载
- npm install --save 包名 （简写： npm i S 包名）
  - 下载并且保存依赖项（package.json 文件中的 dependencies 选项）
- npm uninstall 包名    （npm un 包名）
  - 只删除，如果有依赖项依然保存
- npm unistall --save 包名 （npm un -S 包名）
  - 删除的同时会把依赖项的也删除
- npm help 
  - 查看使用帮助

## 安装 cnpm

项目地址：<https://npm.taobao.org/>

安装`cnpm`替换npm（npm由于源服务器在国外，下载node包速度较慢，cnpm使用国内镜像）：

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

如果我们需要通过 cnpm 去安装一个包时，举例如下：

```
cnpm i vue
```

## 模块化

服务器端规范：

- [**CommonJS规范**](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。

CommonJS 就是一套约定标准，不是技术。用于约定我们的代码应该是怎样的一种结构。


浏览器端规范：

- [**AMD规范**](https://github.com/amdjs/amdjs-api)：是 **[RequireJS](http://requirejs.org/)** 在推广过程中对模块化定义的规范化产出。

```
- 异步加载模块；

- 依赖前置、提前执行：require([`foo`,`bar`],function(foo,bar){});   //也就是说把所有的包都 require 成功，再继续执行代码。

- define 定义模块：define([`require`,`foo`],function(){return});
```

- **[CMD规范]()**：是 **[SeaJS](http://seajs.org/)** 在推广过程中对模块化定义的规范化产出。淘宝团队开发。

```
  同步加载模块；

  依赖就近，延迟执行：require(./a) 直接引入。或者Require.async 异步引入。   //依赖就近：执行到这一部分的时候，再去加载对应的文件。

  define 定义模块， export 导出：define(function(require, export, module){});
```


PS：面试时，经常会问AMD 和 CMD 的区别。


另外，还有ES6规范。

## CommonJS基本语法

### CommonJS 的介绍


[CommonJS](http://www.commonjs.org/)：是 Node.js 使用的模块化规范。

也就是说，Node.js 就是基于 CommonJS 这种模块化规范来编写的。

在 CommonJS 中，每个文件都可以当作一个模块：

- 在服务器端：模块的加载是运行时同步加载的。

- 在浏览器端: 模块需要提前编译打包处理。首先，既然同步的，很容易引起阻塞；其次，浏览器不认识`require`语法，因此，需要提前编译打包。


### 暴露模块的方式

**方式一**（单个成员）：

```javascript
  module.exports = value
```

这个 value 可以是任意的数据类型。

**方式二**（多个成员）：

```javascript
  exports.xxx = value
```

**原理解析**

`exports` 是 `[module.exports]()`  的一个引用

```javascript
console.log(exports === module.exports)   //返回值是 true

exports.foo = 'bar'
// 等价于
module.exports.foo = 'bar'
```

问题**: 暴露的模块到底是谁？

**答案**：暴露的本质是`exports`对象。【重要】

比如，方式二可以理解成是，**给 exports 对象添加属性**。

PS：暴露的关键词是`exports`，不是`export`。

## 常用内置模块

- `path`：处理文件路径。

- `fs`：操作（CRUD）文件系统。

- `child_process`：新建子进程。

- `util`：提供一系列实用小工具。

- `http`：提供 HTTP 服务器功能。

- `url`：用于解析 URL。

- `querystring`：解析 URL 中的查询字符串。

- `crypto`：提供加密和解密功能。


总结：更多内容可以参考 api文档：<https://nodejs.org/api/>


## 文件系统操作

### 相关模块

- fs：基础的文件操作 API

- path：提供和路径相关的操作 API

- readline：用于读取大文本文件，一行一行读

- fs-extra（第三方模块）：<https://www.npmjs.com/package/fs-extra>

## 在Node.js创建一个web服务器

```javascript
// 使用 Node 可以轻松的构建一个 Web服务器

// 在 Node 中专门提供了一个核心模块 http

// 在 http 这个模块的职责就是帮助你编写服务器的

// 1. 加载 http 核心模块
var http = require('http')


// 2. 使用 http.createServer() 方法创建一个Web服务器
  // 返回一个Server 实例
var server = http.createServer()


  //3. 注册 request 请求事件
  // 当客户端请求过来，就会自动触发服务器的 request 的请求事件，然后执行第二个参数： 回调函数
server.on('request', function(){
  console.log('收到客户端的请求了')
})


// 4. 绑定端口号， 启动服务器
server.listen(3000, function() {
  console.log('服务器启动成功了，可以通过 http://127.0.0.1:3000/ 来进行访问')
})
```

