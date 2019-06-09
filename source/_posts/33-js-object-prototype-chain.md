---
title: 33-js-object-prototype-chain
date: 2017-10-19 15:19:06
tags: 33-js-concepts
keywords: prototype，__proto__，对象，原型，原型链，实例与原型关系，构造函数，面向对象程序设计，工厂模式
---
### 对象，原型，原型链
> 分析对象，原型，原型链之间的关系

#### 对象
> 对象来源于两种形式，声明（字面）形式，构造形式

```javascript
// 字面语法
var myobj = {
    key: value,
    ...
}
// 构造形式
var myobj = new Object();
myobj.key = value;
```
构造形式和字面形式是完全同种类的对象，唯一真正的区别是字面可以一次性声明很多key，value，但是构造形式的只能一个个添加
##### 对象的内容存储的位置
> 对象的内容存储在特定的命名位置上，我们成这些为属性，注意<font color="red">实际上对象容器内只存储了属性的名称，它们像指针一样指向值存储的地方</font>

##### 在对象中 属性名<font color="red">总是字符串</font>

##### ES6中加入了计算属性，在字面对象`键`名称位置，可以指定表达式 用`[]`括起来
```javascript
var prefix = 'foo'
var myobj = {
    [prefix + "bar"]: "hello"
}
myobj['foobar']; // 'hello'
```
#### 原型
> 每一个javascript对象（null）除外，在创建的时候就会与之关联另外一个对象，这个对象就是我们所说的原型。每一个对象都会从原型”继承“属性

##### 实例与原型关系
> 当读取属性的时候，如果找不到，就会查找与之关联的原型中的属性，如果还查不到就会再找原型的原型。直到找到最顶层

[prototype 和 __proto__ 详情请戳](/2018/03/29/difficult-prototype-proto/)

#### 原型链
> 原型组成的链状结构，就是原型链

##### 例子讲解
```javascript
function Foo(){
    this.value = 42;
}
Foo.prototype = {
    constructor: Foo,
    method: function() {}
}

function Bar() {}
Bar.prototype = new Foo();
Bar.prototype.constructor = Bar;
Bar.prototype.foo = 'Hello World';

var test = new Bar();
//原型链
test
    Bar.prototype
        { foo: "Hello World" }
            Foo.prototype
                { method: ... };
                    Object.prototype
                        { toString: ... /* etc. */ };
```

#### 构造函数
##### <font color="red">new Dog() 发生了啥</font>
**当 new Dog() 的时候进行的哪些操作**
* 1.创建一个新对象
* 2.新对象执行prototype连接 (实例一旦创建，将自动引用prototype对象的属性和方法)
* 3.将对象绑定到函数调用this
* 4.除非函数返回一个它自己的其他对象，这个被new调用的函数自动返回这个新构建的对象执行new Dog()实际上市返回了一个新对象并赋值给dog1

```javascript
function Dog (name) {
    this.name = name
}
var dog1 = new Dog('dagou');

```
##### 构造函数示例
```javascript
function Person (name, year) {
    this.name = name;
    this.year = year;
    this.sayName = function () {
        alert(this.name);
    }
}
var person1 = new Person('zero', '20');
var person2 = new Person('john', '21');
```
#### 面向对象程序设计

**理解对象**
```javascript
var person = new Object();
person.name = 'zero';
person.age = '20';
person.job = 'web developer';
person.sayName = function () {
    alert(this.name);
}

//=======等价于======

var person = {
    name: 'zero',
    age: '20',
    job: 'web developer',
    sayName: function () {
        alert(this.name)
    }
}
```

#### 创建对象的多种方式以及优缺点

##### 1.工厂模式

> 感觉这是我在日常写重复函数中最长用到的一个啊，比如处理校验，或者处理重复数组之类的，这样的可能会多次遇到的函数 我都会提出到一个util函数里面，需要就直接传入参数，直接调用

```javascript
    function createPerson (name) {
        var o = new Object();
        o.name = name;
        o.getName = function () {
            console.log(this.name)
        }
        return o;
    }

    var person1 = createPerson('zero');
```
> 缺点：对象无法识别，因为所有的实例都指向一个原型

##### 2.构造函数模式
```javascript
    function Person (name) {
        this.name = name;
        this.getName = function () {
            console.log(this.name);
        }
    }
    var person1 = new Person('zero');
```
> 缺点：每次创建实例时，每个方法都要被创建一次
  优点：实例可以识别为一个特定的类型

##### 3.原型模式
```javascript
    function Person (name) {

    }
    Person.prototype.name = 'zero';
    Person.prototype.getName = function () {
        console.log(this.name)
    }
    var person1 = new Person();
```
> 优点：方法不会被重建
  缺点 所有的属性和方法都共享，不能初始化参数

**原型模式优化**
```javascript
  function Person (name) {
  }
  Person.prototype = {
    name : 'zero',
    getName : function () {
        console.log(this.name);
    }
  }
  var person1 = new Person();

```
> 优点：封装性好一点
  缺点： 重写了原型，丢失了constructor属性

##### 4.组合模式
```javascript
function Person (name) {
    this.name = name;
}
Person.prototype = {
    constructor: Person,
    getName: function () {
        console.log(this.name);
    }
    var person1 = new Person();
}
```

> 优点: 该共享的共享，该私有的私有，使用最广泛性
  缺点: 还是不符合有的人想全部写一起，即是最好的封装性

















