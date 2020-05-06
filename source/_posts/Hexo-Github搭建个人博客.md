---
title: Hexo+Github搭建个人博客
date: 2020-02-02 12:58:25
tags: 
    - Github
    - Blog
categories: Github
---


## 0.安装前

- 在安装`Node.js`和`Git`的之前先去了解下Git和Github的基本用法
- 然后再去一步一步的去安装

## 1.安装

### **安装之前先安装 cnpm**

- `npm install cnpm -g --registry=https://registry.npm.taobao.org`
- cnpm是npm的镜像，防止你在用npm下载较慢的情况下可以使用cnpm

### Node.js和Git

- 傻瓜式安装

### 在安装Hexo 

**`npm install hexo-cli -g`  全局安装**

### 查看版本

`node -v`

`npm -v`

`hexo -v`

## 2.创建hexo文件夹下面再建立个blog文件夹   

- 用 `cmd `或 `git bash here `打开
- 初始化我们的博客 `hexo init` 
- 在本地启动hexo  `hexo s` 
  - 启动后就是再本地使用 http://loaclhost:4000 访问
- 如果执行 `hexo s`出现 `ERROR Local hexo not found in G:\XcantloadX` `ERROR Try running: 'npm install hexo --save' ` 错误提示
  - 解决方法：删除文件夹的node_modules文件夹重新执行 `npm install` 或者 `cnpm install`
  - `https://blog.csdn.net/XcantloadX/article/details/78296227 ` 原文博客

## 3.自己新建一篇文章

`hexo n "我的第一篇文章博客"`  创建后 会放置再blog的source\_posts\我的第一篇博客文章.md下

创建文章后进行编辑

然后返回到 blog目录下 敲击  `hexo c`  再敲击 `hexo g`

然后重新启动 `hexo s`

## 4.把本地博客部署到github上

- 到GitHub创建一个仓库
- 然后再blog命令行中安装一个插件
  - `cnpm install hexo-deployer-git --save`

- 到blog的config.yml配置一些相关的配置
  - 找到deploy 添加三个选项
  - type: 'git'
  - repo: github仓库的地址
  - branch: master

- 然后部署到远端 `hexo d`

- 然后就可以通过 类似  https://flingyp.github.io/  的格式访问
  - 你自己创建仓库时命名的

## 5.更换Hexo的主题

### 5.1安装主题

- 到主题的Github下 复制它的地址
- 然后再你们的blog文件夹下打开终端输入
  - ` git clone 刚才复制的地址 themes/xxxx `
  - xxxx 是主题名

### 5.2使用主题

-  修改博客根目录下的 `_config.yml` 文件，注释掉原来的 theme 并新增一句 `theme: xxxx` （注意冒号后面有空格） 

### 5.3然后现在本地预览下

先执行 `hexo clear`

`hexo g`

再通过 `hexo s`

 打开 http://localhost:4000/ 预览效果 

### 5.4再部署到GitHub上

`hexo clear`

`hexo g`

`hexo d`

然后就可以进行访问了

---

## 命令简写

hexo n '我的博客' === hexo new '我的博客'    #建立新的文章

hexo g === hexo generate        #生成

hexo s === hexo server            #启动服务预览

hexo d === hexo deploy           #部署

hexo c === hexo clean               #清除缓存

## 解决hexo博客解决不蒜子统计无法显示问题
[网址](https://www.jianshu.com/p/fd3accaa2ae0)

## 如果出现了换电脑了或者是电脑坏了的情况下 需要在其他电脑继续布置你的博客的话

+ 可以在自己的Github另外建个仓库用来存放你的Hexo源码，每次更新了自己的博客同时也去更新你的Hexo源码
+ 在出现上面的情况后可以`git clone xx`克隆你的Hexo源码
+ 克隆后 在你 `hexo init` 完毕后  可以将你的 Hexo 源码里的 `scaffolds`、`source`、`themes`、`_config.yml` 文件替换掉你新的Hexo里的这四个文件 即可



