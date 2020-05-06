---
title: less预处理器
date: 2020-04-13 09:32:34
tags: 
    - HTML5 CSS3
categories: HTML5 CSS3
---

# Less

> Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。   Less 可以运行在 Node 或浏览器端

+  http://lesscss.cn

##  Variables  变数

+ 申明一些常用变量

```less
@backgroungColor: blue;
@baseColor: #ccc;
#header {
  color: @baseColor;
  background-color: @backgroungColor;
}
```

## Mixins 混合蛋白

+ 我们可以定义一些公用的类 放到 其他类中使用

```less
// Mixins 公用的类
.bordered {
  border-top: solid 10px pink;
  border-bottom: solid 12px palevioletred;
}

#header {
  width: 100px;
  height: 100px;
  color: @baseColor;
  background-color: @backgroungColor;
  .bordered();  // 使用
}
```

## Operations

+ 变量也可以进行运算

```less
@backgroungColor: blue;
@baseColor: #ccc;
@baseWidth: 100px;
@widthOperations: @baseWidth + 20px;

#header {
  width: @widthOperations; // Operations
  height: 100px;
  color: @baseColor;
  background-color: @backgroungColor;
  &:hover{
    background-color: #34495e;
  }
}
// 也可以对颜色进行算数运算 
@color: #224488 / 2; //results in #112244
background-color: #112244 + #111; // result is #223355
```

## Escaping  转义

+ 允许将任意字符串用作属性或变量值

```less
@backgroungColor: blue;
@baseColor: #ccc;
@baseWidth: 100px;
@widthOperations: @baseWidth + 20px;
@min768: ~"(max-width: 500px)"; // 转义

#container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
}

#header {
  width: @baseWidth;
  height: 100px;
  color: @baseColor;
  background-color: @backgroungColor;
  &:hover {
    background-color: #34495e;
  }
  @media @min768 {      // 书写格式
    font-size: 20px;
    color: red;
  }
}
// 输出结果
@media (max-width: 500px) {
    #header {
        font-size: 20px;
        color: red;
    }
}
```

## Namespaces and Accessors 命名空间和访问器

+ 有时，出于组织目的或为了提供一些封装，您可能希望对混合包进行分组。 您可以在Less中直观地做到这一点。

```less
@backgroungColor: blue;
@baseColor: #ccc;
@baseWidth: 100px;
@baseHeight: 100px;
@baseFontSize: 20px;
@widthOperations: @baseWidth + 20px;
@min768: ~"(max-width: 500px)";

#container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
}

#base {
  .base {
    text-align: center;
    text-decoration: none;
    background: #f1c40f;
    font-size: @baseFontSize;
  }
}
// 假设我们想用 #base .base的类  就可以这样用
#header {
  width: @baseWidth;
  height: @baseHeight;

  #base.base();  // 使用
}
```

## Maps

+ 从Less 3.5开始，您还可以将mixin和规则集用作值的映射。

```less
#colors() {
    primary: blue;
    secondary: green;
}

.button {
    color: #colors[primary];
    border: 1px solid #colors[secondary];
}

// output 
.button {
    color: blue;
    border: 1px solid green;
}
```

## Import 导入文件

```less
@import "library"; // library.less
@import "typo.css";
```

