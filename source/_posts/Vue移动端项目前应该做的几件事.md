---
title: Vue移动端项目前应该做的几件事
date: 2020-03-12 16:13:45
tags: 
    - Vuejs
categories: Vuejs
---

1. 因为项目是移动端的网页 所以要加入下面这行代码

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0" minimum-scale=1.0 maximum-scale=1.0 user-scalable=no>
```

2. 引入 reset.css 文件 重置页面的样式表。 不同手机的浏览器上默认些的样式是不统一的。
3. 引入 border.css 文件

- 该css样式用于解决移动端1像素边框问题。问题分析：有些手机的屏幕分辨率较高，是2-3倍屏幕。css样式中border:1px solid red;在2倍屏下，显示的并不是1个物理像素，而是2个物理像素。为了解决这个问题，引入border.css是非常有必要的 

- 网上提供的文件源码：  https://blog.csdn.net/gm0125/article/details/91390885   reset.css  border.css

4. 安装第三方模块 fastclick

- 移动设备上的浏览器默认会在用户点击屏幕大约延迟300毫秒后才会触发点击事件，这是为了检查用户是否在做双击。为了能够立即响应用户的点击事件 我们需要在项目上安装一个第三方模块包  fastclick`  并且引入它

- `cnpm install fastclick --save`

- ```javascript
  import fastClick from 'fastclick'
  fastClick.attach(document.body)
  ```

