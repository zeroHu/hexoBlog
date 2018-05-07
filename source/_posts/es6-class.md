---
title: es6-class
date: 2018-01-01 09:58:26
tags: ES6
---
### class
> javascript 中，生成实例对象的传统方法是通过构造函数

```javascript
    function Point(x, y) {
        this.x = x
        this.y = y
    }
    Point.prototype.toString = function () {
        return '(' + this.x + ',' + this.y + ')' 
    }
```
上面的这种写法是传统的写法 与c语言 java语言相差很大，很容易让新学者误解，es6提供了更接近与传统写法的形式，引入了class这个概念
```javascript
    class Point {
        constructor(x, y) {
            this.x = x
            this.y = y
        }
        toString() {
            return '(' + this.x + ',' + this.y + ')' 
        }
    }
    // 分解

    class Point2 {
        doStuff() {
            console.log('it is dostuff')
        }
    }
    typeof(Point2) //"function"
    Ponit2 === Point2.prototype.constructor

    let p = new Point2()
    p.doStuff() // it is dostuff
    // 构造函数的prototype属性，在es6类上面继续存在，事实上类的所有方法都定义在prototype属性上面
```
上面的代码定义了一个”类“，里面的constructor方法，就是构造方法。this代表实例对象，也就是Es5的Point方法对应Es6de Point 方法

> 由于类的方法都添加在prototype上面，所有类的新方法可以添加在prototype对象上面，Object.assign方法可以很方便的一次向类添加多个方法

```javascript
    class Point {
        constructor() {

        }
    }
    Object.assign(Point.prototype, {
        toString(){

        },
        toValue(){

        }
    })
    // 证明是不可枚举的
    Object.keys(Point.prototype) //[]
    Object.getOwnPropertyNames(Point.prototype) //["constructor","toString"]

    var Es5Fn = function (x, y) {
        this.x = x
        this.y = y
    }
    Es5Fn.prototype.toString = function () {
        //...
    }
    Object.keys(Es5Fn.prototype) // ["toString"]
    Object.getOwnPropertyName(Es5Fn.prototype)
```
> **注意点是：类的内部所有定义的方法，都是不可枚举的（non-enumerable） **

类的属性名可以采用表达式
```javascript
    let methodName = 'getArea'
    class Square {
        constructor(length){

        }
        [methodName](){

        }
    }
```

#### 严格模式
> 类和模块的内部，默认就是严格模式，所以不需要使用”use strict“制定运行模式。只要你的代码写在类或者模块之中

#### constructor
> constructor 方法是类的默认方法，通过new 命令生成的对象实例，自动调用该方法，一个类必须有construcotr方法，如果没有显示定义。一个空的constrctor方法会自动被添加

```javascript
    class Point {

    }
    // 等同于
    class Point {
        constructor() {

        }
    }
```
#### 函数class表达式
```javascript
    const MyClass = class Me {
        getClassName() {
            retrun Me.name
        }
    }
    // 需要注意的这个类名 是MyClass 而不是Me,Me只在Class内部代码可用，指代当前类
    const MyClass = class { /* ... */ };
```

#### Class的取值函数（getter）和存值函数（setter）
```javascript
    class MyClass {
        constructor() {

        }
        get prop() {
            return 'getter'
        }
        set prop(value) {
            console.log('setter is:' + value)
        }
    }
    let inset = new MyClass()
    inset.prop = 123 // setter is:123
    inset.prop // getter
```
#### Class的Generator的方法
如果在某个方法之前加上星号(*) 就表示该方法是一个Generator函数

```javasript
class Foo {
    constructor(...args) {
        this.args = args;
    }
    * [Symbol.iterator]() {
        for (let arg of this.args) {
            yield arg;
        }
    }
}

for (let x of new Foo('hello', 'world')) {
    console.log(x);
}
// hello
// world
```
#### Class 的静态方法 static
类相当于原型，所有在类中定义的方法都会被实例继承，如果在一个方法前加上static关键字，表示该方法不会被继承。
```javascript
    class Foo {
        static classMethod() {
            return 'hello'
        }
    }
    // 调用法师Foo.classMethod() 而不是在Foo的实例上调用
    注意：如果静态方法包含this关键字，这个this指的是类，而不是实例
```
#### Class的静态属性和实例属性
静态属性指的是Class本身的属性，Class.protoName 而不是定义在实例对象（this）上的属性
```javascript
    class Foo {

    }
    Foo.prop = 1
    Foo.prop // 1
```
### class继承
> class 可以通过extends关键字实现继承，这比es5通过修改原型链实现继承，要更加的清晰和方便

#### 简介
```javascript
    class Point {
    }
    class ColorPoint extends Point {
        constructor(x, y, color) {
            super(x, y) //调用父类的constructor(x, y)
            this.color = color
        }
        toString() {
            return this.color + ' ' + super.toString() //调用父类的super
        }
    }
    上面的代码定义了一个ColorPoint 类，该类通过extends 继承了Point类的属性和方法
    ColorPoint 新建constructor  是为 ColorPoint 新建this 如果没有这个  这里面的this 就是父类的this
    ColorPoint 中出现了super 表示了父类的this的意思
```
同时需要注意的是 父类的静态方法也会被子类继承
#### Object.getPrototypeOf()
> Object.getPrototypeOf方法可以用来从子类上获取父类

```javascript
    Object.getPrototypeOf(ColorPoint) === Point //true
    因此这个方法可以用来判断某个类是否继承另外一个类
```
#### super 关键字
> super关键字既可以当做函数使用，也可以当做对象使用。

```javascript
    // 作为函数
    class A {

    }
    class B extens A {
        constructor() {
            super()
        }
    }
```

```javascript
// 作为对象
class A {
  p() {
    return 2;
  }
}

class B extends A {
  constructor() {
    super();
    console.log(super.p()); // 2
  }
}

let b = new B();
```