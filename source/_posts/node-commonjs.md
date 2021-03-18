---
title: node-commonjs
date: 2020-03-17 21:57:17
tags: node
---

### nodejs 模块规范

#### script

-   脚本变多，手动管理加载顺序
-   不动脚本之间的逻辑调用，需要管理全局变量。不易管理
-   没有 html 怎么办，没法加载 script

#### commonjs 模块规范 起源

-   javscript 社区发起，nodejs 上应用并推广
-   影响到浏览器端 JavaScript

#### commonjs 介绍

-   定义：每个文件就是一个模块，有自己的作用域。在一个文件里面定义变量，函数，类，都是私有的。对其他文件是不可见的。
-   特点：1）所有代码都运行在模块作用域，不会污染全局作用域。2）模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接读取缓存结果。要想让模块再次运行，必须清除缓存。3）模块加载的顺序，按照其在代码中出现的顺序。

a.js

```javascript
var x = 10;
var addX = function (value) {
    return value + x;
};
moudule.exports = {
    x,
    addX,
};
```

b.js

```javascript
// 需要加载a.js
var ajs = require("a.js");
a.addX(10); //15
```

上面代码中，变量 x 和函数 addX，是当前文件特有的私有，其他文件不可见
