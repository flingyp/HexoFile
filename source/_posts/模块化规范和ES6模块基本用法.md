---
title: 模块化规范和ES6模块基本用法
date: 2020-02-04 18:37:32
tags: 
    - ES6
categories: ES6
---

# 模块化的相关规范

## 1.模块化的概述

**传统的开发模式主要问题**

- 命名冲突
- 文件依赖

**通过模块化就可以解决上诉的问题**

-  模块化就是把单独的一个功能封装到一个模块（文件）中，模块之间相互隔离，但是可以通过特定的接口公开内部成 员，也可以依赖别的模块 

- 模块化开发的好处：方便代码的重用，从而提升开发效率，并且方便后期的维护 

## 2.模块化的规范

### 浏览器的模块化规范

- AMD 、CMD     

### 服务器的模块化规范

- CommonJS     例如:  `Node.js` 就是遵守CommonJS规范的

### 浏览器和服务器通用的模块化规范

- ES6模块化
  - ES6 语法规范中，在语言层面上定义了 ES6 模块化规范，是浏览器端与服务器端通用的模块化开发规范。
  - ES6模块化中定义：
    - 每个js文件都是独立的模块
    - 导入模块成员使用 `import` 关键字
    - 导出模块成员使用 `export` 关键字

# ES6模块化的基本语法

### 导出

语法：export  导出成员

```javascript
// 可向外导出变量
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;
export { firstName, lastName, year };
export let s1 = 'aaa';

// 可向外导出个函数
export function say(x,y) {
    return x + y;
}
```



### 导入

语法：  import { s1 } from '模块文件路径' 

```javascript
// 导入模块成员
 import { s1, s2 as ss2, say } from './m1.js' 
```



### 默认导出与导入

- 默认导出语法： export default 默认导出的成员 

- 默认导入语法： import 接收名称 from '模块标识符
- 注：导入的接收名称可以自己命名



### 直接导入并执行模块的代码

- 有时候，我们只想单纯执行某个模块中的代码，并不需要得到模块中向外暴露的成员，此时，可以直接导入并执行模块代码

```javascript
import '模块文件路径'
```

