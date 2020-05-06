---
title: hexo之自定义域名
date: 2020-02-05 20:21:28
tags: 
    - Github
    - Blog
categories: Github
---

> 如果不想要Github提供的域名的话我们可以选择使用自己的域名



1.首先应该去购买一个域名。可以去 阿里云、  华为云、  腾讯云什么的都可以去看看逛逛

2.购买完域名后就进行DNS域名解析。我是在阿里云买了个 .top 的域名贼便宜 .com太贵了

3.进行域名解析主要添加以下内容：

-  点击添加解析，记录类型选A或CNAME，A记录的记录值就是ip地址，github(官方文档)提供了两个IP地址，`192.30.252.153  和  192.30.252.154`，这两个IP地址为github的服务器地址，两个都要填上，解析记录设置两个www和@，线路就默认就行了，CNAME记录值填你的github博客网址 。

4.在你的本地博客的文件根目录下  添加一个文件名叫 CNAME的文件。 注意不需要后缀

5.在CNAME文件中 就写上 自己购买的域名名字 例如我的： yyblog.top 

- 注意：不要写   www.yyblog.top   ，那么以后你只能用www.yyblog.top访问 
  - 如果写的是 yyblog.top ，那么  那么用www.yyblog.top和yyblog.top访问都是可以的 

6.打开 cmd 清理 hexo  重新发布到 github上



之后就可以通过自己的域名来访问了。

 