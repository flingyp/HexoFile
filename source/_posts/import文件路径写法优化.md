---
title: import文件路径写法优化
date: 2020-03-12 16:12:09
tags: 
    - Vuejs
categories: Vuejs
---

在Vue中我们常常要引入公用的文件，但是我们加入文件所在的位置路径相对较远的时候，我们去引入文件 文件路径写的就比较长。所以我们需要做代码优化。



在Vue中文件中 `import '文件路径'` 有时候这个文件路径相对较长 这时候可以定义一个`别名` 来定义一段指定的路径。当我们引入文件路径的时候 就可以使用这个 别名 来替代这个指定的路径。



比如   有个 comon文件夹  里面存放了  font.styl 文件 这时候我们需要引入这个文件 我们可以这么做：

- 给这个 common文件夹 路径位置 取个别名   就叫 com

- 这时候我们引入只需要 `import 'com/font.styl'`即可

这样不管你文件的位置 和 font.syul文件 位置 相对多远 都可以这样引入。

当然我们别名的定义需要在  `webpack.base.conf.js` 文件的 `resolve` 对象 的 `alias` 去定义

```javascript
resolve: {
    extensions: ['.js', '.vue', '.json'],
        alias: {
            'vue$': 'vue/dist/vue.esm.js',
             '@': resolve('src'),
             'common': resolve('src/common')
            // @ 代表 src目录  common 代表 src/common目录  
        }
},
```

