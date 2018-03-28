---
title: this
date: 2018-03-28 15:34:57
tags: js 困惑
---
### this
#### ES5 this
> <font color="red">**function被作为method调用时，this指向调用对象。**</font>

##### <font color="#0099ff">默认绑定</font>，也就是直接调用前面不带任何对象 eg: test(), (function() {})()
> 其实这种可以看为是 `Global.test()` `Global.(function() {})()` 所以调用对象可以看为Global 如果再浏览器就是window

```javascript
var x = 1;
function test() {
    this.x = 2;
}
test();
alert(x); // 2
```

##### 作为<font color="#0099ff">对象的方法</font>被调用
> 函数作为对象里面的某个方法，被调用的时候，这时的this指向上级对象。

```javascript
var x = 1;
function test () {
    alert(this.x)
}
var o = {
}
o.x = 2;
o.fn = test;
o.fn(); // 2
```
##### 作为<font color="#0099ff">构造函数</font>被调用
> 所谓构造函数其实就是，通过这个函数生成一个新的对象，this指向这个对象

```javascript
var x = 1;
function test() {
    this.x = 2;
}
var test1 = new test();
alert(test1.x); // 2
alert(x); // 1 证明this 不是window  如果是window 就是2
```
##### <font color="#0099ff">call()调用 或者 apply()调用</font>
> `apply`和`call`是函数对象的一个方法，它的作用是改变函数的调用对象，它的第一个参数就表示改变后调用这个函数的对象。所以 `this`指的是第一个对象

```javascript
var x = 1;
function test () {
    alert(this.x);
}
var o = {};
o.x = 2;
o.fn = test;
var obj = {};
obj.x = 3;
o.fn.apply(); // 1
o.fn.call(obj); //3
```

##### 当调用点适合上面4中规则的时候，<font color="#0099ff">优先级处理</font>
* 第一优先级: **new 构造函数**
* 第二优先级: **call apply**
* 第三优先级: **对象的方法**
* 第四优先级: **默认绑定**

#### ES6 this
> <font color="red">**箭头函数es6 内部的this指向，是由上下文决定**</font>

##### 栗子证明
这个是 es5 的this
```javascript
var x = 'i am window';
function test() {
    function foo() {
        console.log(this.x)
    }
    foo()
}
var o = {};
o.x = 'i am o'
o.fn = test;
o.fn(); // 'i am window'
```
这个是es6的this
```javascript
var x = 'i am window';
function test() {
    var foo = () => {
        console.log(this.x)
    }
    foo()
}
var o = {};
o.x = 'i am o'
o.fn = test;
o.fn(); // 'i am o'
```

