---
title: 闭包 和 匿名函数
date: 2018-03-29 17:58:56
tags: 33-js-concepts
keywords: js closures, anonymous function，闭包，匿名函数
---
### 闭包和匿名函数的区别和关系，使用场景

#### 闭包
> <font color="blue">就是在一个函数内部创建另一个函数。或者说闭包是函数的嵌套，就是内层的函数可以访问外层函数的所有变量，即使外层函数已经执行完毕（涉及到javascript的作用域链）【忘了谁的博客】</font>
  <font color="#ff9090">闭包就是当一个函数即使是在它的词法作用域外被调用时，也可以记住并访问它的词法作用域。【you don't know js】</font>
  <font color="red">闭包指的是有权访问另一个函数作用域中的变量 【js 高程】</font>

##### 典型的闭包示例
```javascript
var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f;
}

var foo = checkscope();
foo();

// 分析一下
ES = [globalContext, checkscopeContext, fContext]
fContext.scope = [AO, checkscopeContext.AO, globalContext.VO]
```
##### 闭包解决之难题
```javascript
// 闭包只能取得包含函数中任何变量的最 后一个值
function jisu () {
    var result = [];
    for (var i =0; i<10; i++) {
        result[i] = function () {
            return i;
        }
    }
    result[8](); //10
}
// 改成能够实现的函数
function jisu () {
    var result = [];
    for (var i =0;i<10;i++) {
        result[i] = function (num) {
            return function () {
                return num;
            }
        }(i)
    }
    result[8](); //8
}
// 闭包写外面
function jisu () {
    function test(i) {
        return function() {
            console.log(i)
        }
    }
    var result = [];
    for (var i=0; i<10; i++) {
        result[i] = test(i)
    }
    result[8](); //8
}
```
##### 原文地址
> [原文地址](https://github.com/mqyqingfeng/Blog/issues/9)

#### 匿名函数
> javascript中最灵活的一种对象，最简单的理解就是：没有名字的函数

##### 栗子
```javascript
function () {
    return 'hello'
}

(function() {
    alert('something')
})()

(function() {
    alert('other')
}())
```

##### 立即执行函数表达式(IIFE)
> [原文链接](https://segmentfault.com/a/1190000003985390)

```javascript
// 这两种模式都可以被用来立即调用一个函数表达式，利用函数的执行来创造私有变量
(function(){/* code */}());// Crockford recommends this one，括号内的表达式代表函数立即调用表达式
(function(){/* code */})();// But this one works just as well，括号内的表达式代表函数表达式
```
