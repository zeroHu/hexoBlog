---
title: es6-module
date: 2018-01-01 15:58:19
tags: ES6
---
### module
#### 简介
> 历史上，JavaScript一直没有模块（module）体系，无法将一个程序拆分为互相依赖的小文件，再用简单的方法拼装起来，其他语言都有这个功能。比如 ruby 有reqire Python有import css 都有@import，再es6定制之前 社区定制了一些模块加载方案，最主要有commonjs 和 amd 两种，前者用于服务器，后者用于浏览器，es6在语言标准层面上。实现了模块功能。
  es6模块的设计思想，是尽量的静态化，是编译时确认模块的依赖关系，以及输出和输入变量。commonjs 和 amd模块，都只能运行时确定这些东西，比如 commonjs 模块就是对象，输入时必须查找对象属性。

```javascript
    // commonjs 模块
    let { stat, exists, readFile } = require('fs')
    // 等同于
    let _fs = require('fs')
    let stat = _fs.stat
    let exists = _fs.exists
    let readFile = _fs.readFile
    // 上面的代码实质上是 整体加载fs 模块 （即加载fs的所有方法）,生成一个对象（_fs)，然后再从这个对象中读取3个方法，这种加载称为 ”运行时加载“ ， 是因为只有在运行的时候才能得到这个对象，导致完全没有办法在编译时做 ”静态优化“
```
ES6 模块不是对象，而是通过export 命令显示指定输出代码，再通过import 导入
```javascript
    import { stat, exists, readFile } from 'fs'
    // 上面的代码的实质是从 fs 模块加载3个方法，其它方法都不加载。这种加载方法叫做 ”编译时加载“ 或者 静态加载。即ES6 可以在编译时就完成模块加载， 效率要比commonjs 模块加载的方式高，当然 这也导致了没法引用es6 模块本身，因为它不是对象
```
#### 严格模式
> ES6 自动采用严格模式，不管你在头上有没有添加 ” use strict “

**严格模式主要有以下限制**
    -：变量必须声明后再使用
    -：函数的参数 不能有同名属性 否则报错
    -：不能使用 `with` 语句
    -：不能对只读属性赋值，否则报错
    -：不能使用前缀0 表示八进制数，否则报错
    -：不能删除不可删除的属性，否则报错
    -：不能删除 `delete prop` ，或报错，只能删除 `delete global[prop]`
    -：`eval` 不会在它的外层作用域引入变量
    -：`eval` 和 `arguments` 不能被重新赋值
    -：`arguments` 不会自动反应参数的变化
    -：不能使用 `arguments.callee`
    -：不能使用 `arguments.caller`
    -：禁止 `this` 指向全局对象
    -：不能使用 `fn.caller` 和 `fn.arguments` 获取函数调用的堆栈
    -：添加了保留字 如：`protected、static和interface`

#### export命令
> 模块的功能主要由两个命令构成，`export` 和 `import`，`export`命令用于规定模块的对外接口，`import` 命令用于输入其它模块提供的功能

一个模块就是一个独立的文件，该文件内部的所有变量，外部无法获取到，如果你希望外部能获取到这个模块的某个变量，就必须使用`export`导出变量

```javascript
    export var firstName = 'hu'
    export var lastName = 'zero'
    export var year = 1990

    // 或者
    // 这种写法更推荐 因为可以在 export 中看到本模块全部导出的变量
    var firstName = 'hu'
    var lastName = 'zero'
    var year = 1990
    export { firstName, lastName, year }

    // exprt 还可以用来直接导出函数
    export function multiply(x, y) {
        return x*y
    }
```
#### import 
> 使用 `export` 命令定义了模块的对外接口，其它js文件 就可以通过`import` 命令记载这个模块

```javascript
    import { firstName, lastName, year } from '../xxx.js'
    // 或者 模块的整体加载
    import * as getMyDetail from './circle';
    getMyDetail.firstName //这样调用
```
#### export default 
> 从前面的例子可以看出，使用import命令的时候，用户需要知道所要加载的变量名或函数名，否则无法加载。但是，用户肯定希望快速上手，未必愿意阅读文档，去了解模块有哪些属性和方法。

```javascript
    // export-default.js
    export default function () {
        console.log('foo')
    }
    // 或者
    function foo() {
        console.log('foo')
    }
    export default foo

    // import-default.js
    import customName from './export-deafult.js'
    customName() // 'foo'
```


