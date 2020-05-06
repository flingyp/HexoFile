---
title: Vue中import文件路径代码优化
date: 2020-02-16 14:07:57
tags: 
    - Vuejs
categories: Vuejs
---

## import 文件路径代码优化

> 在Vue中我们引入一个模块文件时候会使用到 `import '文件路径'` 这个语法

但是当我们引入的模块过多的时候一些文件路径又太长就会显得整个 import 部分 太多太杂

这个时候我们就需要对 import 部分做代码优化让 import 部分看过去很清除

1. 在使用 Vue-cli 脚手架2.x版本创建项目的时候   在文件结构 bulid文件夹下有个 `webpack.base.conf.js` 文件在这个文件下我们可以定义一个`别名` 来定义一段指定的路径

webpack.base.conf.js文件中默认是这样的

```javascript
resolve: {
    extensions: ['.js', '.vue', '.json'],
        alias: {
            'vue$': 'vue/dist/vue.esm.js',
             '@': resolve('src')    
        }
},
```

这里的 **alias对象** 中 @ 就代表 src这个目录。 

```javascript
import '@/../../'
```

当我们出现文件路径有一些常用的路径我们就可以在这定义这里举个例子：

```javascript
resolve: {
    extensions: ['.js', '.vue', '.json'],
        alias: {
            'vue$': 'vue/dist/vue.esm.js',
             '@': resolve('src'),
              // 这里我们定义了 styles别名 来替换这段路径 src/assets/styles
             'styles': resolve('src/assets/styles')
        }
},
    
    
// 在文件中 引入文件时
import 'styles/reset.css'   ===    import 'src/assets/styles/reset.css'
import 'styles/border.css'  ===    import 'src/assets/styles/border.css'
import 'styles/iconfont.css'  ===  import 'src/assets/styles/iconfont.css'

// 注意： 在Vue单文件组件中 写CSS样式区域中 要引入文件 前面要有@符合， 路径开头要加上 ~
@import '~styles/varibles.styl';
```

当我们修改了 `webpack.base.conf.js`文件的内容 这个时候项目会报错 这个时候要重新启动项目