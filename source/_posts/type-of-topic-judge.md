---
title: type-of-topic-judge（类型判断）
date: 2017-12-12 14:32:55
tags: javascript
---
#### 类型判断

> 原文地址:https://github.com/mqyqingfeng/Blog/issues/28

在日常的工作中，只要有业务和逻辑需求必然会用到类型判断，判断是否是数字 数组 对象等然后做下一步是非常常见的事情，今日就让我们来一探如何来正确的判断类型，让你的代码运行起来不报错

##### typeof
相信这货大家都用到过，我之前也用到过，但是貌似总有一点心虚，不知道这样判断是否能保证所有的情况下都能正常运行。
> js 的类型 ： string number boolean object undefined null

这几个分别对应用typeof来判断的时候得结果是：
```javascript
    typeof 'zero' //"string"
    typeof 21 //"number"
    typeof true //"boolean"
    typeof {} //"object" typeof []//"object" typeof Function //"function"
    typeof undefined //"undefined"
    typeof null //"object"
```
问题就非常容易总结出来就是，typeof 能判断string number undefined但是不能判断object null  和 object种类里面的细节

##### Object.prototype.toString
如何来理解这个函数呢

> 1.If the this value is undefined, return "[object Undefined]".
  2.If the this value is null, return "[object Null]".
  3.Let O be the result of calling ToObject passing the this value as the argument.
  4.Let class be the value of the [[Class]] internal property of O.
  5.Return the String value that is the result of concatenating the three Strings "[object ", class, and "]".

总结就是 调用Object.prototype.toString 返回的是”[object“ 和 class 和 ”]“组成的字符串，而class 是我们要判断的对象的内部属性

还是按照上面的js 类型用 Object.prototype.toString来判断
```javascript
    Object.prototype.toString.call('zero');//"[object String]"
    Object.prototype.toString.call(21);//"[object Number]"
    Object.prototype.toString.call(true);//"[object Boolean]"
    Object.prototype.toString.call([]);//"[object Array]"  Object.prototype.toString.call({});//"[object Object]"   Object.prototype.toString.call(function a(){});//"[object Function]"
    Object.prototype.toString.call(undefined);//"[object Undefined]"
    Object.prototype.toString.call(null);//"[object Null]"



    object 类的拓展
    var date = new Date();
    Object.prototype.toString.call(date) // [object Date]
```


既然这货能够判断这么仔细，应该封装一个函数 ，便于调用判断类型啊。

```javascript
// 第二版
var class2type = {};

// 生成class2type映射
"Boolean Number String Function Array Date RegExp Object Error".split(" ").map(function(item, index) {
    class2type["[object " + item + "]"] = item.toLowerCase();
});

function type(obj){
    if(obj === null){
        return obj+"";
    }
    return typeof obj ==="object" || typeof obj === "function" ? class2type[Object.prototype.toString.call(obj)] || "object" : typeof obj;
}



可以利用type来封装函数罗

var isFunction = function (obj){
    return type(obj) === 'function'
}

var isArray = function(obj){
    if(Array.isArray){
        return Array.isArray(obj)
    }else{
        return type(obj) === 'array'
    }
}

```