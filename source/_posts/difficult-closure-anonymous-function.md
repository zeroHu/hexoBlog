---
title: 闭包 和 匿名函数
date: 2018-03-29 17:58:56
tags: js 困惑
---
### 闭包和匿名函数的区别和关系，使用场景

#### 闭包
> 闭包指的是有权访问另一个函数作用域中的变量，创建闭包的常见方式，就是在一个函数内部创建另一个函数。或者说闭包是函数的嵌套，就是内层的函数可以访问外层函数的所有变量，即使外层函数已经执行完毕（涉及到javascript的作用域链）

```javascript
//典型的闭包示例
function createComparisonFunction (protypeName) {
    return function (object1, object2) {
        var value1 = object1[protypeName];
        var value2 = object2[protypeName];
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            return 0;
        }
    }
}
//常见的一个问题
//闭包只能取得包含函数中任何变量的最 后一个值
function jisu () {
    var result = [];
    for (var i =0; i<10; i++) {
        result[i] = function () {
            return i;
        }
    }
}
//改成能够实现的函数
function jisu () {
    var result = [];
    for (var i =0;i<10;i++) {
        result[i] = function (num) {
            return function () {
                return num;
            }
        }(i)
    }
}
```
#### 匿名函数
> javascript中最灵活的一种对象，最简单的理解就是：没有名字的函数

未完待续...