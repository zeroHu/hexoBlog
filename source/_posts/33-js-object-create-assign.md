---
title: 33-js-object-create-assign
date: 2019-06-11 15:35:43
tags: 33-js-concepts
keywords: object.create, object.assign
---
### Object.create
> `Object.create()`方法创建创建一个新对象，使用现在的对象来提供新创建的对象的`__proto__`
> 语法： Object.create(proto_obj, [properties]), proto: 新创建对象的原型， propertiesObject（可选）添加到新创建对象的可枚举属性（即自身定义的属性，而不是其原型链上的枚举属性）

```javascript
const person = {
  isHuman: true,
  printIntroduction: function() {
    console.log(`hello, my name is zero and is human ? ${this.isHuman}`)
  }
}

const me = Object.create(person); // 这里将新创建一个 {}, 且me的__proto__指向 person的 __proto__, 所以当me[key] 会沿着__proto__向上找.
me.isHuman // true
me.name = "zero"
me.printIntroduction(); // hello, my name is zero and is human ? true

me.name // zero
person.name // undefined


// 添加上properties的看看
const other = Object.create(person, {sex: {value: "female", writable: true, enumerable: true, configurable: true}})
```

**Object.create 实现类继承**
```javascript
function Shape () {
  this.x = 0;
  this.y = 0;
}
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.log('shape moved')
}

// Rectangle 继承 Shape开始
function Rectangle() {
  Shape.call(this)
}
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
// Rectangle 继承 Shape结束

var rect = new Rectangle(); 
console.log(rect instanceof Rectangle) // true
console.log(rect instanceof Shape) // true
react.move(1,2) // shape moved
```
**es5 或者以前版本 polyfill Object.create**
```javascript
if (typeof Object.create !== 'function') {
  Object.create = function (proto_obj, propertiesObject){
    if (typeof proto_obj !== 'object' && typeof proto_obj !== 'function') {
      throw new TypeError('object prototype may only be an object' + proto_obj)
    } else if (proto_obj === null) {
      throw new TypeError('this browser implementtaion of Object.create is a shim and not support null as first argument')
    }
    if (typeof propertiesObject != 'undefined') {
      throw new Error("This browser's implementation of Object.create is a shim and doesn't support a second argument.");
    }

    function F(){}
    F.prototype = proto_obj
    return new F();
  }
}
```
### Object.assign
> `Object.assign()`方法用于将所有可枚举属性的值从一个或多个源对象赋值到目标对象。它将返回目标对象。
> 语法：Object.assign(target, ...sources); // target : 目标对象， sources: 源对象. 
> 1.如果目标对象中有源对象相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。
> 2.`Object.assign`方法只会拷贝源对象本身的并且可枚举的属性到目标对象。 注意： `Object.assign` 不会跳过 `null` 或 `undefined`
> 3.`Object.assign`方法只是浅拷贝，


```javascript
const target = {a: 1, b: 2}
const source = {a: 2, c: 3}
const source2 = {d: 4, f: 6};
const returnTarget = Object.assign(target, source); // {a: 2, b:2, c: 3}
target // {a: 2, b:2, c: 3}
const returnTarget = Object.assign(target, source, source2); // {a: 2, b:2, c: 3, d: 4, f: 6}

```
**拷贝symbol类型的属性**
```javascript
const o1 = {a: 1}
const o2 = {[Symbol("foo")]: 2}

const obj = Object.assign({}, o1, o2); // {a: 1, Symbol(foo): 2} and error in some version firefox
```
**继承属性和不可枚举属性不可拷贝**
```javascript
const obj = Object.create({
  foo: 1
}, {
  bar: {
    value: 2
  },
  baz: {
    value: 3,
    enumerable: true // 是个可枚举属性
  }
})
const copy = Object.assign({}, obj); // {baz: 3}
```
**原始类型会被包装成对象**
注意，只有字符串的包装对象才可能有自身可枚举属性。
```javascript
const v1 = "abc"
const v2 = true
const v3 = 10
const obj = Object.assign({}, v1, null, v2, undefined, v3, v4); // null 和 undefined 会被忽略   {0: "a", 1: "b", 2: "c"}
```

**es5 或更早以前的polyfill**
```javascript
if (typeof Object.assign !='function') {
  // must be writable: true, enumerable: false, configurable: true
  Object.defineProperty(Object, "assign", {
    value: function assign(target, varArgs) { // .length of function is 2
      "use strict"
      if (target == null) {
        throw new TypeError('cannot convert undefined or null to object');
      }
      let to = Object(target);
      for (var index = 1; index < arguments.length; index++) {
        var nextSource = arguments[index];
        if (nextSource != null) {
          for (let nextKey in nextSource) {
            if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
              to[nextKey] = nextSource[nextKey];
            }
          }
        }
      }
      return to;
    },
    writable: true,
    configurable: true
  })
}
```
**reference doc**
> [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create)