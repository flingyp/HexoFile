---
title: webpack的使用
date: 2020-02-04 20:43:50
tags: 
    - Webpack
categories: webpack
---

# Webpack

## Webpack概述

- webpack是一个流行的**前端项目构建工具（打包工具）**

- webpack 提供了**友好的模块化支持**，以及**代码压缩混淆、处理 js 兼容问题、性能优化**等强大的功能，从而把写代码的重心放到具体的功能实现上，提高了开发效率和项目的可维护性。 

- [官方网址]( https://www.webpackjs.com/ )

## Webpack基本使用步骤

前提条件：

1. 在开发一个项目的前提下

- 新建项目空白目录 运行 `npm init -y` ，初始化包管理配置文件 package.json 
- 新建 src 源代码目录 
- 新建 src -> index.html 首页 
- 初始化首页基本的结构

2.再安装Webpack

- 安装Webpack	
  - `npm install webpack webpack-cli –D`
  - 安装 webpack 和 webpack-cli 
- 在项目根目录中，创建名为 `webpack.config.js` 的 webpack 配置文件

- 在 webpack 的配置文件中，初始化如下基本配置： 

```javascript
module.exports = {   
    mode: 'development' 
    // mode 用来指定构建模式  还有一个模式是 production
    // development 为 开发模式 一般开发使用 development
    // production 为产品发布模式 会压缩文件
}
```

-  在 package.json 配置文件中的 scripts 节点下，新增 dev 脚本如下：

```javascript
"scripts": {  
    "dev": "webpack" 
    // script 节点下的脚本，可以通过 npm run 执行 
} 
```

- 在终端中运行 `npm run dev` 命令，启动 webpack 进行项目打包

## 配置打包的入口和出口

webpack 的 4.x 版本默认规定：

- 打包的文件对象为： src文件夹下的index.js文件
- webpack打包后的文件放在为：dist文件夹下的main.js文件 

如果要修改打包的入口与出口，可以在 webpack.config.js 中新增如下配置信息： 

```javascript
const path = require('path') 
// 导入 node.js 中专门操作路径的模块 
module.exports = {   
    entry: path.join(__dirname, './src/index.js'), 
    // 打包入口文件的路径   
    output: {     
        path: path.join(__dirname, './dist'), 
             // 输出文件的存放路径     
        filename: 'bundle.js' 
        	// 输出文件的名称   
    } 
}
```

## 配置webpack自动打包功能

当你修改项目的被打包的文件后，因为在页面 script 标签引用的是 webpack 打包过后的文件所以要执行一次 `npm run dev` 才能生效。这样就显的有些麻烦

所以要配置 自动打包 功能

-  运行 `npm install webpack-dev-server –D` 命令，安装支持项目自动打包的工具 
- 修改 package.json -> scripts 中的 dev 命令为：

```javascript
"scripts": {   
    "dev": "webpack-dev-server" 
    // script 节点下的脚本，可以通过 npm run 执行 
}

// 配置自动打包的相关参数
 // package.json中的配置   
// --open 打包完成后自动打开浏览器页面   
// --host 配置 IP 地址   
// --port 配置端口   
"scripts": { 
    "dev": "webpack-dev-server --open --host 127.0.0.1 --port 8888" 
}, 
```

- 将 src文件中index.html中，script 脚本的引用路径，修改为 "/被打包文件名字“ 
- 运行 `npm run dev` 重新进行打包 
- 在浏览器中访问 http://localhost:8080 地址，查看自动打包效果
- 之后只要修改了被打包文件的代码 然后 保存了 就是自动打包

注意点：

- webpack-dev-server 会启动一个实时打包的 http 服务器 

- webpack-dev-server 打包生成的输出文件，默认放到了项目根目录中，而且是虚拟的、看不见的 
  - 所以要修改脚本的引用路径

## 配置 html-webpack-plugin 生成预览页面 

配置好后 访问 http://localhost:8080 地址 会看到项目的页面

- 运行 npm install html-webpack-plugin –D 命令，安装生成预览页面的插件 

- 修改 webpack.config.js 文件头部区域，添加如下配置信息： 

 ```javascript
// 导入生成预览页面的插件，得到一个构造函数 
const HtmlWebpackPlugin = require('html-webpack-plugin') 
const htmlPlugin = new HtmlWebpackPlugin({ 
    // 创建插件的实例对象   
    template: './src/index.html', 
    // 指定要用到的模板文件   
    filename: 'index.html' 
    // 指定生成的文件的名称，该文件存在于内存中，在目录中不显示 })
 ```

- 修改 webpack.config.js 文件中向外暴露的配置对象，新增如下配置节点： 

```javascript
module.exports = {   
    plugins: [ htmlPlugin ] 
    // plugins 数组是 webpack 打包期间会用到的一些插件列表 
} 
```

