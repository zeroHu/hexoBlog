---
title: class-array-object（类数组对象）
date: 2017-12-08 15:17:13
tags: javascript
---
#### 类数组对象

类数组对象定义
> 拥有一个length属性，和若干索引属性的对象

> tips:要说到类数组对象，Arguments 对象就是一个类数组对象。在客户端 JavaScript 中，一些 DOM 方法(document.getElementsByTagName()等)也返回类数组对象。

例子
```
    //这是一个数组
    var array = ['name','age','sex'];
    //这是一个类数组
    var arraylike = {
        0:'name',
        1:'age',
        2:'sex',
        length:3
    }

```
为啥叫类素组是吧？接下来我们从读写，获取长度，遍历等这三个方面来查看这两个对象

读写
```
    读：
    console.log(array[0]);//name
    console.log(arraylike[0]);//name
    写:
    array[0] = 'new name';
    arraylike[0] = 'new name';
```

获取长度

```
    array.length;//3
    arraylike.length;//3
```

遍历

```
    for(var i = 0, len = array.length; i < len; i++) {
       ……
    }
    for(var i = 0, len = arrayLike.length; i < len; i++) {
       ……
    }
```
#### 接下来改来点不太一样的了，不然这两货就没有必要拿出来了，也没有累数组干脆叫数组得了，分啥啊。

```
    array.push('4');//['name','age','sex','4']
    arrayLike.push('4');// 报错 arrayLike.push is not a function
```

#### 那类素组要如何才能当做数组放心的使用呢

既然无法直接调用，那么我们就可以用Function.call 间接调用


直接出几个 能将类数组转为数组的方法
```
    var arrayLike = {0: 'name', 1: 'age', 2: 'sex', length: 3 }
    // 1. slice
    Array.prototype.slice.call(arrayLike); // ["name", "age", "sex"] 
    // 2. splice
    Array.prototype.splice.call(arrayLike, 0); // ["name", "age", "sex"] 
    // 3. ES6 Array.from
    Array.from(arrayLike); // ["name", "age", "sex"] 
    // 4. apply
    Array.prototype.concat.apply([], arrayLike)
```

