---
title: webpack处理非js模块
date: 2020-02-05 15:00:30
tags: 
    - Webpack
categories: webpack
---

## 通过 loader 打包 非js模块

在实际开发过程中，**webpack** 默认**只能打包处理以 .js 后缀名结尾的模块**，其他非 .js 后缀名结 尾的模块，webpack 默认处理不了，**需要调用 loader 加载器**才可以正常打包，否则会报错！ 

官方文档：` https://www.webpackjs.com/loaders/ `

### 打包CSS文件

1.安装处理 css 文件的 loader

- `npm install style-loader --save-dev`
- `npm install --save-dev css-loader`
  - 可以合并成 :  ` npm i style-loader css-loader -D `

2.在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则

```javascript
// 所有第三方文件模块的匹配规则   
module: { 
    rules: [ 
        { test: /\.css$/, use: ['style-loader', 'css-loader'] } 
    ] 
}
// test 指的是匹配的文件类型  use 表示对应要调用的 loader
// css-loader 负责将css文件进行加载  style-loader 复杂将样式添加到DOM中
```

3.注意点

- use 数组中指定的 loader 顺序是固定的 
- 多个 loader 的调用顺序是：从后往前调用 



### 打包处理 less 文件  和 scss 文件

-  运行 `npm i less-loader less -D` 命令 
  - 处理 less 的  
- 在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则

```javascript
// 所有第三方文件模块的匹配规则   
module: { 
    rules: [ 
      { test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] } 
    ] 
  }
```

**处理 scss文件就类似**

- 运行 `npm i sass-loader node-sass -D` 命令 
- 在 webpack.config.js 的 module -> rules 数组中，添加 loader 规则

```javascript
// 所有第三方文件模块的匹配规则   
module: { 
    rules: [ 
      { test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] } 
    ] 
  }
```



### 打包样式表中图片和字体文字文件

- 运行 `npm i url-loader file-loader -D` 命令 

- 在 webpack.config.js文件中 module对象的rules添加 loader规则

```javascript
module: { 
    rules: [ 
        {  
            test: /\.jpg|png|gif|bmp|ttf|eot|svg|woff|woff2$/,  
            use: 'url-loader?limit=16940' 
        } 
    ] 
}
// use选项中 ？后面的是 loader 的参数项
// limit 用来指定图片的大小，单位是字节(byte),只有小于 limit 大小的图片，才会被转为 base64 图片
```



### ES6语法转换为ES5语法

-  安装babel转换器相关的包：

```shell
npm i babel-loader @babel/core @babel/runtime -D 
```

- 安装babel语法插件相关的包：

```shell
npm i @babel/preset-env @babel/plugin-transformruntime  @babel/plugin-proposal-class-properties –D 
```

- 在项目的根目录中，创建 babel 的配置文件 名字为 `babel.config.js` 并初始化基本配置

```javascript
 module.exports = { 
     presets: [ '@babel/preset-env' ], 
     plugins: [ '@babel/plugin-transform-runtime', '@babel/plugin-proposal
               class-properties’ ] 
 }
```

- 在 webpack.config.js 文件中 添加 loader 规则

```javascript
// exclude 为排除项，表示 babel-loader 不需要处理 node_modules 中的 js 文件   
{ test: /\.js$/, use: 'babel-loader', exclude: /node_modules/ } 
```

