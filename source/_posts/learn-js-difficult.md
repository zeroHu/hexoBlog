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