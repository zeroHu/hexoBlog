---
title: prototype __proto__ 的区别和联系
date: 2018-03-29 11:08:53
tags: js 困惑
---
### prototype和__proto__
> `__proto__ `(隐式原型) ， `prototype`(显示原型)

#### `protype` (显示原型)
> <font color="red">只有函数有prototype属性</font>，每一个函数在创建之后都会拥有一个prototype属性。这个属性指向函数的原型对象。（Function.prototype.bind方法构造的函数除外）

##### 作用
> 用来实现基于原型的继承和属性的共享

#### `__proto__` (隐式原型)
> javascript中任意对象（null除外）都有一个内置属性，prototype，es5之前没有标准的方法，但是大多数浏览器支持`__proto__`来访问，或者用ES5的`Object.getPrototypeOf()`

##### 作用
> 构成原型链，同样用于实现基于原型的继承。eg:当我们obj.x 的时候如果再obj中找不到，就会沿着`__proto__`接着找

##### <font color="red">指向</font>
> <font color="red">`__proto__`指向创建这个对象的函数的显式原型。</font>

#### `prototpye` 和 `__proto__` 关系
> `__proto__`指向**创建**这个对象的函数的`prototype`

#### 几个重要点
* js万物皆对象，方法（function）是对象，方法的原型（Function.prototype）是对象，对象都具有`__proto__`,一个对象的隐式原型指向构造该对象的构造函数的原型
* 方法是一个特殊的对象，除了和其他对象一样拥有`__proto__`属性以外，还有自己独特的属性(原型`prototype`),这个属性是一个指针，指向一个对象，这个对象的用途是<font color="red">包含所有实例共享的属性和方法，我们把这个对象叫做<font color="green">原型对象</font></font>


#### 终极大图
![proto关系图](http://www.zeroyh.cn/images/prototype.jpg)