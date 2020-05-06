---
title: Vue-Router的基本使用
date: 2020-02-03 15:35:14
tags: 
    - Vuejs
categories: Vuejs
---
# 核心插件-Vue-Router

### 路由的基本概念与原理 

#### 路由

- 路由是个比较广义和抽象的概念，**路由的本质就是对应关系**
- 在开发中，路由分为：
  - 前端路由
    - 根据**不同的用户事件**，显示不同的页面内容（用户事件和事件处理函数之间的对应关系）
    - **SPA 单页面应用程序最核心的技术点就是前端路由**
  - 后端路由
    - 根据不同URL请求，后端响应不同的内容（URL请求地址和服务器的对应关系）

### vue-router的基本使用 

> Vue Router（官网： https://router.vuejs.org/zh/ ）是 Vue.js 官方的路由管理器。 它和 Vue.js 的核心深度集成，可以非常方便的用于SPA单页面应用程序的开发。 
>
> 关于 SPA单页面应用程序 在 Vuejs的初步了解有提到
>
> Vue Router 还有更多的功能可以去官方查看文档

#### Vue Router 包含的功能有：

-  支持HTML5 历史模式或 hash 模式 
-  支持嵌套路由 
-  支持路由参数 
-  支持编程式路由 
-  支持命名路由

#### 基本使用步骤

- 安装

  ```npm
  npm install vue-router
  ```

- 引入相关的**库文件**

  ```javascript
  // 注意顺序
  <!-- 导入 vue 文件，为全局 window 对象挂载 Vue 构造函数 -->   
  <script src="./lib/vue_2.5.22.js"></script> 
  
  <!-- 导入 vue-router 文件，为全局 window 对象挂载 VueRouter 构造函数 --> 
  script src="./lib/vue-router_3.0.2.js"></script> 
  ```

- 添加**路由链接**

  ```javascript
  <!-- router-link 是 vue 中提供的标签，默认会被渲染为 a 标签 --> 
  <!-- to 属性默认会被渲染为 href 属性 --> 
  <!-- to 属性的值默认会被渲染为  开头的 hash 地址 --> 
  
  <router-link to="/user">User</router-link> 
  <router-link to="/register">Register</router-link> 
  ```

  

- 添加**路由填充位**

  ```javascript
  <!-- 路由填充位（也叫做路由占位符） --> 
  <!-- 将来通过路由规则匹配到的组件，将会被渲染到 router-view 所在的位置 --> 
  <router-view></router-view> 
  ```

  

- 定义路由**组件**

  ```javascript
  // 1. 定义 (路由) 组件。
  // 可以从其他文件 import 进来
  var user = { 
      template: '<div>User</div>' 
  } 
  var reg = { 
      template: '<div>reg<div>' 
  } 
  ```

  

- 配置**路由规则**并且**创建路由实例**

  ```javascript
  // 创建路由实例对象     
  var router = new VueRouter({     
      // routes 是路由规则数组     
      routes: [       
          // 每个路由规则都是一个配置对象，其中至少包含 path 和 component 两个属性：       		  // path 表示当前路由规则匹配的 hash 地址       
          // component 表示当前路由规则对应要展示的组件       
          {path:'/user',component: User}, 
          {path:'/register',component: Register} 
      ] 
  })
  ```

  

- 路由**挂载到Vue根实例**中

  ```javascript
  new Vue({ 
     el: '#app',      
     // 为了能够让路由规则生效，必须把路由对象挂载到 vue 实例对象上  
     // router: router
     router 
  });
  ```
  
  

