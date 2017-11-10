---
title: lear-js-difficult
date: 2017-10-19 15:19:06
tags: javascript 比较复杂的部分
---
#### 原型链
```
function Foo(){
    this.value = 42;
}
Foo.prototype = {
    method:function(){}
}

function Bar(){}
Bar.prototype = new Foo()
Bar.prototype.foo = 'Hello World';
Bar.prototype.constructor = Bar;

var test = new Bar()

//原型链
test
    Bar.prototype
        {foo:"Hello World"}
            Foo.prototype
                {method: ...};
                    Object.prototype
                        {toString: ... /* etc. */};
```
#### 构造函数
```
function Person(name,year){
    this.name = name;
    this.year = year;
    this.sayName = function(){
        alert(this.name);
    }
}
var person1 = new Person('zero','20');
var person2 = new Person('john','20');
```
#### 闭包
> 闭包指的是有权访问另一个函数作用域中的变量，创建闭包的常见方式，就是在一个函数内部创建另一个函数
```
典型的闭包示例
function createComparisonFunction(protypeName){
    return function(object1,object2){
        var value1 = object1[protypeName];
        var value2 = object2[protypeName];
        if(value1<value2){
            return -1;
        }else if(value1>value2){
            return 1;
        }else {
            return 0;
        }
    }
}
常见的一个问题
闭包只能取得包含函数中任何变量的最 后一个值
function jisu(){
    var result = [];
    for(var i =0;i<10;i++){
        result[i] = function(){
            return i;
        }
    }
}
改成能够实现的函数
function jisu(){
    var result = [];
    for(var i =0;i<10;i++){
        result[i] = function(num){
            return function(){
                return num;
            }
        }(i)
    }
}
```
#### 面向对象程序设计
```
理解对象
var person = new Object();
person.name = 'zero';
person.age = '20';
person.job = 'web developer';
person.sayName = function(){
    alert(this.name);
}

=======等价于======

var person = {
    name: 'zero',
    age: '20',
    job: 'web developer',
    sayName: function(){
        alert(this.name)
    }
}
```


















