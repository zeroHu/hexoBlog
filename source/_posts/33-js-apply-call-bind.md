---
title: 33-js-apply-call-bind
date: 2019-05-09 16:44:04
tags: 33-js-concepts
---
### how to use apply, call, bind 
> when I want to write this blog, I feel so sad, because I know how to use, but I cannot not explain why so? and involving this and prototype ...

#### how to use `call` or `Function.prototype.call`

> fun.call(thisArg, arg1, arg2, arg3...) // thisArg is the fun function execute this point, if not sent thisArg or null || undefined then the this will be point global.this

```javascript
var obj = {
  a: 1
}
function findVal() {
  return this.a
}

// if you want the findVal function show 1, how should you do ? 
console.log(findVal.call(obj)) // 1
```

#### how to use `bind` or `Function.prototype.bind`
simple example
```javascript
var obj = {
  a: 1,
  findVal: function() {
    return this.a
  }
}
// now we can think about if we execute obj.findVal() what you expect the end ? is 1?
console.log(obj.findVal()) // 1


var showVal = obj.findVal;
// now you can once again think about the answer , is also 1?
console.log(showVal()); // undefined 

// how should we make the showVal function is correct ? 

// now !!! we can use bind. bind can make the showVal functions this point obj
var showValBind = obj.findVal.bind(obj);

console.log(showValBind()); // 1

```

** refrence doc **
> [MDN call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
> [MDN apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
> [MDN bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
> [lvan sifrim](https://medium.com/@ivansifrim/the-differences-between-call-apply-bind-276724bb825b)
> [niladri sekhar dutta](https://www.codementor.io/niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)
> [mqyqingfeng](https://github.com/mqyqingfeng/Blog/issues/11)