---
title: 33-js-factories-classes
date: 2019-06-10 21:45:57
tags: 33-js-concepts
keywords: 工厂模式，构造模式，类
---
### constructor functions
> constructor function name method is Pascal Notation

```javascript
// Camel Notation: oneTwoThreeFour
// Pascal Notation: OneTwoThreeFour
function CreateCircle(a) {
    this.a = a
}
const Circle1 = new CreateCircle(1); // {a: 1, show: function() {console.log('show)}}
const Circle2 = new CreateCircle(2); // {a: 2, show: function() {console.log('show)}}
CreateCircle.prototype.newkey = "hello world";
CreateCircle.prototype.getName = function() {
    console.log('name', this.a);
}
Circle1.newkey // hello world
```
whenever a new function created in javascript, javascript engine by default adds a `prototype` property to it, this property is an object and we call it `prototype object`. by default this prototype object has a construtor property which points back to our function, and other property `__proto__`which is an object
![function prototype](http://static.zeroyh.cn/WechatIMG1007.png)
**every new constructor such as Circle1, Circle2 will has a `__proto__` assign to the CreateCircle prototype**
### factor functions
```javascript
function facotryCreateCircle(a) {
    return {
        a,
        getName() {
            console.log('name', a)
        }
    }
}
const one = facotryCreateCircle(1) // {a: 1, getName: function(console.log('name', 1))}
```
### classes
#### define
> the classes is smilar to construtor functions. 

```javascript
class CreateCircle {
    construtor(a) {
        this.a = a
    }
    getName() {
        console.log('name', this.a);
    }
}
const Circle1 = new CreateCircle(1); // {a: 1, show: function() {console.log('show)}}
CreateCircle(2) // TypeError, class constructor function cannot be invoked without 'new'
CreateCircle.prototype.newkey = "hello world"
```
#### classes need attention
* classes function methods are non-enumerable. in javascript each property of an object has `enumberable` flag, which define its availability for some operations to be performed on that property.
* if you don't want to add `construtor` to class function, default will add a empty `constructor() {}`
* classes function inside code always `use strict`
* classes declarations are not `hosited` (变量不会提升).
* classes dont't allow the property value assignments lick constructor functions or object literals.

#### classes feature
##### constructor

* constructor is a speical function for classes what represents class itself. when you new a class instance. the constructor is automatically called.
* one classes cannot have more than one constructor
* a constructor can use `super` keyword to call the constructor of the class its extending from.

##### static methods
* static methods are functions on class itself. and not on its prototype. unlike the other methods in the class. which are define on its `prototype`
* remember that static method cannot be called from the class instance. 

```javascript
class Vehicle {
    constructor(make, model, color) {
        this.make = make;
        this.model = model;
        this.color = color;
    }
    getName() {
        return this.make + " " + this.model;
    }
    static getColor(v) {
        return v.color;
    }
}
let car = new Vehicle("Honda", "Accord", "Purple");
Vehicle.getColor(car); // "purple"
// !!!! cannot called car.getColor() !!!!!
```

##### getter/setter
> to get or set property value

```javascript
class Vehicle {
    constructor(model) {
        this.model = model;
    }
    
    get model() {
        return this._model;
    }

    set model(value) {
        this._model = value;
    }
}
```

* under the hood, the getter and setter defined on the class `prototype`

##### Subclassing
> subclassing is a way you can implement inheritance in javascript classes. keyword `extends` is used to create a child class of a class

```javascript
class Vehicle {
    constructor(make, model, color) {
        this.make = make;
        this.model = model;
        this.color = color;
    }
    getName () {
        return this.make + " " + this.model;
    }
}
class Car extends Vehicle {
    getName () {
        return this.make + " " + this.model + "in child class";
    }
}
let car = new Car("tie", "huxing", "red")
car.getName(); // tie huxing in child class
//=============== or ================

class Car extends Vehicle {
    getName () {
        return super.getName() + " called in child class"
    }
}

let car = new Car("tie", "huxing", "red")
car.getName(); // tie huxing called in child class

```

**reference doc**
> [es6 class](https://www.javascriptjanuary.com/blog/es6-classes)
[tajawal](https://medium.com/tech-tajawal/javascript-classes-under-the-hood-6b26d2667677)

