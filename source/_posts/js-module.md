---
title: js-module
date: 2018-04-11 11:08:05
tags: javascript
---
### javascript 模块理解
> 模块的产生可以让代码更加容易维护，可读性和简洁性更强。命名空间增大，所谓模块化是指的解决代码分割，作用域隔离，模块之间的依赖管理以及发布到生产环境时的自动化打包和处理等

#### CommonJS
> commonjs 中设置的规范是：
1.每个javascript文件都是一个独立的模块上下文。在这个上下中默认创建的属性都是私有的。
2.commonjs规范主要适用于服务器端编程，所以采用同步加载模块的策略。如果我们依赖多个模块，会一个个依次加载。
3.这个方案主要包含`require`和`module`这两个关键字，允许模块对外暴露接口并有其它模块使用

示例
```javascript
// file sayHello.js
function sayHello () {
    this.hello = function () {
        console.log('hello');
    }
    this.sayGoodBye = function () {
        console.log('goodbye');
    }
}
module.exports = sayHello;
// file main.js
var Say = require('./sayHello.js')
var says = new Say();
says.hello();
```
<font color="red">node支持commonjs的模块化写法</font>
#### AMD
> amd(Asynchronous Module Definition)即异步模块定义：
1.amd优先照顾浏览器的模块加载场景，使用了异步加载和回调的方式。
2.amd和commonjs一样需要脚本加载器，尽管amd只需要对`define`方法支持，`define`需要三个参数：模块名称，模块运行和需要依赖数组，所有依赖都可用之后执行的函数(该函数按照依赖声明的顺序，接收依赖作为参数)
3.`define`既是一种引用模式，也是一种定义模块的方式。

示例
```javascript
// file lib/sayHello.js
define(function () {
    return {
        sayHello: function() {
            console.log('hello')
        }
    }
})
// file lib/sayGoodBye.js
define(function () {
    return {
        sayGoodBye: function() {
            console.log('bye')
        }
    }
})

// file main.js
define(['./lib/sayHello.js','./lib/sayGoodBye.js'], function (sayH, sayG) {
    // 执行之前 sayHello.js, sayGoodBye.js已经异步加载完成
    sayH.sayHello();
    sayG.sayGoodBye();
})
```
**RequireJs**
requirejs 是遵循的`AMD`规范，requirejs 要求每个独立模块都放在独立的文件中，按照是否有其它情况分为独立和非独立模块。

示例
```javascript
// 独立模块 不依赖其他模块。直接定义
define(function () {
    return {
        a: function () {
        },
        b: function () {
        }
    }
})
// 等价于
define({
    a: function () {
    }，
    b: function () {
    }
})

// 非独立模块，对其他模块有依赖
define([ 'moduleOne', 'moduleTwo' ], function(mOne, mTwo){
    ...
});
```
#### CMD
> cmd中一个模块就是一个文件
1.全局函数define，用来定义模块
2.参数factory，可以是一个函数，也可以是对象或者字符串
3.当factory为对象、字符串时，

示例
```javascript
// 定义json数据模块
define({ "json": "data" })
// factory为函数 表示模块的构造方法，执行构造方法便可以得到模块向外提供的接口。
define(function (require, exports, module) {
    // 模块代码
})
```
**SeaJS**
1.遵循CMD规范，与node模块一样的写法
2.依赖自动加载，配置简洁

示例
```javascript
 // 加载一个模块 
seajs.use('./a');

// 加载模块，加载完成时执行回调
seajs.use('./a'，function(a){
    a.doSomething();
});

// 加载多个模块执行回调
seajs.use(['./a','./b']，function(a , b){
    a.doSomething();
    b.doSomething();
});
```

#### UMD
> 统一模块定义UMD,是将AMD和CommonJs合在一起的尝试

```javascript
(function(define) {
    define({
        a: function() {
            
        }
    })
})(
    typeof module === 'object' && module.exports && typeof define !== 'function' ? function (factory) {
        module.exports = factory()
    } : define
)
```

#### ES6模块
> [详情链接](/2018/04/10/es6-export-import/)

#### 参考资料
> [segmentfault](https://segmentfault.com/a/1190000012464333)


