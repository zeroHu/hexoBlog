---
title: 33-js-closures-anonymous-function
date: 2018-03-29 17:58:56
tags: 33-js-concepts
keywords: js closures, anonymous function，闭包，匿名函数
---
### 闭包和匿名函数的区别和关系，使用场景

#### 闭包
> <font color="blue">就是在一个函数内部创建另一个函数。或者说闭包是函数的嵌套，就是内层的函数可以访问外层函数的所有变量，即使外层函数已经执行完毕（涉及到javascript的作用域链）【忘了谁的博客】</font>
> <font color="#ff9090">闭包就是当一个函数即使是在它的词法作用域外被调用时，也可以记住并访问它的词法作用域。【you don't know js】</font>
> <font color="red">闭包指的是有权访问另一个函数作用域中的变量 【js 高程】</font>
> <font color="#333">a closure is the combination of a function and the lexical environment within which that function was declared. and i'm sure that you have use closure in your code everywhere. maybe you don't know that but it's obvious. </font>【MDN】

#### closure code and what happened
```javascript
function createCounter() {
    let counter = 0
    const myFunction = function() {
        counter = counter + 1
        return counter
    }
    return myFunction
}
const increment = createCounter()
const c1 = increment()
const c2 = increment()
const c3 = increment()
console.log('example increment', c1, c2, c3)
```
Now that we got the hang of it from the previous two examples, let’s zip through the execution of this, as we expect it to run.

* Lines 1–8. We create a new variable createCounter in the global execution context and it get’s assigned function definition.
* Line 9. We declare a new variable named increment in the global execution context..
* Line 9 again. We need call the createCounter function and assign its returned value to the increment variable.
* Lines 1–8 . Calling the function. Creating new local execution context.
* Line 2. Within the local execution context, declare a new variable named counter. Number 0 is assigned to counter.
* Line 3–6. Declaring new variable named myFunction. The variable is declared in the local execution context. The content of the variable is yet another function definition. As defined in lines 4 and 5.
* Line 7. Returning the content of the myFunction variable. Local execution context is deleted. myFunction and counter no longer exist. Control is returned to the calling context.
* Line 9. In the calling context, the global execution context, the value returned by createCounter is assigned to increment. The variable increment now contains a function definition. The function definition that was returned by createCounter. It is no longer labeled myFunction, but it is the same definition. Within the global context, it is labeledincrement.
* Line 10. Declare a new variable (c1).
* Line 10 (continued). Look up the variable increment, it’s a function, call it. It contains the function definition returned from earlier, as defined in lines 4–5.
* Create a new execution context. There are no parameters. Start execution the function.
* Line 4. counter = counter + 1. Look up the value counter in the local execution context. We just created that context and never declare any local variables. Let’s look in the global execution context. No variable labeled counter here. Javascript will evaluate this as counter = undefined + 1, declare a new local variable labeled counter and assign it the number 1, as undefined is sort of 0.
* Line 5. We return the content of counter, or the number 1. We destroy the local execution context, and the counter variable.
* Back to line 10. The returned value (1) gets assigned to c1.
* Line 11. We repeat steps 10–14, c2 gets assigned 1 also.
* Line 12. We repeat steps 10–14, c3 gets assigned 1 also.
* Line 13. We log the content of variables c1, c2 and c3.

**the closure is a collection of all the variables in scope at the time of createion of the function**

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
**reference doc**
> [参考地址](https://github.com/mqyqingfeng/Blog/issues/9)
> [dailyjs clousure 特别好的文！必看](https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8)
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
> [jsinfo](https://zh.javascript.info/closure)