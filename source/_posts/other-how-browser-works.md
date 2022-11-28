---
title: how-browser-works
date: 2018-03-27 11:16:46
tags: other
keywords: 浏览器的工作原理， how browser works
---
### 图解browser work
#### 当你向浏览器地址栏输入http://www.google.com会发生什么呢
* Resolve DNS
* Request Page
* Tokenize the response
* Parse HTML
* Build Dom tree
* Build Render tree
* Layout the Render tree
* Painting

#### Dns LookUp
> 输入的域名 -> 本地DNS服务器 -> 根DNS服务器 -> 本地域名服务器将ip发送到客户端主机

![原理图](http://upload.zeroyh.cn/dns-look.jpg)
#### Request a Page
> 请求回来的二进制数据 -> 解析为字符 -> 解析成dom

![原理图](http://upload.zeroyh.cn/request-page.jpg)

#### PARSE, RENDER, LAYOUT & PAINT
> 解析html为dom 树结构(parsing html to construct the dom tree) -> 渲染树结构(render tree construction) -> 将结构布局到位置上(layout of the render tree) -> 绘制GUI整个结构(painting the render tree)

render tree: DOM TREE + CSS == RENDER TREE
![layout 图解](http://upload.zeroyh.cn/render.jpg)

#### 地址
> http://arvindr21.github.io/howBrowserWorks/#/