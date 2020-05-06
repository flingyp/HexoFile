---
title: Nodemon自动重启服务工具
date: 2020-02-02 19:21:17
tags: 
    - NodeJS
categories: Node.js
---

## 修改完代码自动重启

> 我们可以使用第三方命令行工具， `nodemon` 可以解决频繁修改代码重启服务器问题

`nodemon`  是一个基于Node.js开发的一个第三方命令行工具，使用的时候需要独立安装

```shell
npm install --global nodemon
#--global 全局
#在任意目录执行该命令都可以
# nodemon --version  查看版本号
```

安装完毕后然后使用：

```shell
#以前执行 js文件 是 
node xx.js

#安装了 nodemon 后 执行js文件 使用 nodemon
nodemon xx.js
```

只要通过 `nodemon xx.js`  启动服务，则它会监视你的文件变化，当你的文件发生变化的时候会自动帮助你重启服务器

