---
title: Vue脚手架的基本使用
date: 2020-02-03 15:35:14
tags: 
    - Vuejs
categories: Vuejs
---
## 1.Vue 脚手架概述

> Vue 脚手架用于**快速生成 Vue 项目基础架构**
>
> 官方网址： https://cli.vuejs.org/zh/ 

## 2.安装

安装 3.x 版本的Vue脚手架

```npm
npm install -g @vue/cli
```

检查版本号

```npm
vue -V   
```

## 3.Vue脚手架创建vue项目（三种）

> 创建项目 官方有一些详细的说法可以去查看

#### 3.1基于  交互式命令行 的方式创建

```javascript
vue create my-project
// 项目名字必须为英文
```

#### 3.2基于 图形化界面 的方式创建

```javascript
vue ui
```

#### 3.3 基于 2.x 的版本模板 创建

```npm
npm install -g @vue/cli-init
```

```javascript
vue init webpack my-project 
// 项目名字必须为英文
```



## 4.初始创建好的项目文件结构

![脚手架创建项目文件结构](C:\Users\LEGION\Desktop\前端\Vue.js\vue-imgs\脚手架创建项目文件结构.png)

[![1zl0VP.png](https://s2.ax1x.com/2020/02/15/1zl0VP.png)](https://imgchr.com/i/1zl0VP)



## 5.Vue脚手架的自定义配置（两种方式）

#### 1.通过 package.json 配置

```javascript
// 必须是符合规范的json语法   
"vue": { 
    "devServer": { 
        "port": "8888", 
        "open" : true 
    } 
},
```

#### 2.单独创建配置文件来配置项目  (推荐)

> 因为 package.json 主要用来管理包的配置信息；为了方便维护，推荐将 vue 脚 手架相关的配置，单独定义到 vue.config.js 配置文件中

- 在项目的跟目录创建文件 vue.config.js 

- 在该文件中进行相关配置，从而覆盖默认配置 

```javascript
// vue.config.js 
module.exports = { 
    devServer: { 
        port: 8888,
        open: true
    } 
}
```



## 附： 创建好Vue项目怎么引用 Element-UI 组件库

 安装：`npm i element-ui -S`

 导入 Element-UI 相关资源

```javascript
// 导入组件库   
import ElementUI from 'element-ui';   
// 导入组件相关样式   
import 'element-ui/lib/theme-chalk/index.css';   // 配置 Vue 插件   
Vue.use(ElementUI);
```

