---
title: 33-js-apply-call-bind
date: 2019-05-09 16:44:04
tags: 33-js-concepts
keywords: apply, call, bind
---
### how to use apply, call, bind 
> when I want to write this blog, I feel so sad, because I know how to use, but I cannot not explain why so? and involving this and prototype ...

#### how to use `call` or `Function.prototype.call`

> fun.call(thisArg, arg1, arg2, arg3...) // thisArg is the fun function execute this point, if not sent thisArg or null || undefined then the this will be point global.this

```javascript
var obj = {
  a: 1
}
function findVal(a, b) {
  return this.a + a + b
}

// if you want the findVal function show 1, how should you do ? 
console.log(findVal.call(obj, 1, 2)) // 4
```

#### how to use `apply` or `Function.prototype.apply`
> function.apply(thisArg, [argArray]), and the apply is similar call, just change the arg1, arg2, ... to argArray

```javascript
var obj = {
  a: 1
}
function findVal(a, b) {
  return this.a + a + b
}

// if you want the findVal function show 1, how should you do ? 
console.log(findVal.apply(obj, [1,2])) // 4
```

#### how to use `bind` or `Function.prototype.bind`
> function.bind(thisArg, arg1, arg2, arg3)
  `bind` create a new function return that, when called, has its `this` keyward set to the provided value
  
**simple example**

```javascript
var obj = {
  a: 1,
  findVal: function(m, n) {
    return this.a + m
  }
}
// now we can think about if we execute obj.findVal() what you expect the end ? is 1?
console.log(obj.findVal()) // 1


var showVal = obj.findVal;
// now you can once again think about the answer , is also 1?
console.log(showVal()); // undefined 

// how should we make the showVal function is correct ? 

// now !!! we can use bind. bind can make the showVal functions this point obj
var showValBind = obj.findVal.bind(obj, 20, 30);

console.log(showValBind()); // 51


// bind functions can execute twice now we can use bind do more
 var showValBind2 = obj.findVal.bind(obj, 20);
 console.log(showValBind2(30)); // 51 
//  now you know bind can separate the arguments just like function(arg1)(arg2)
```

### how to similate a function bind

#### similate bind
> from how to use bind we know bind features is can back a function and recive arguments.

```javascript
// we can use apply to similate bind solve the `this` point
// now if we chat use simBind realize the top `showValBind2` return value. what should we write for the simBind ?
// first time
Function.prototype.simBind = function(context) {
  const self = this;
  return function() {
    return self.apply(context)
  }
}
// now test 
var obj = {
  a: 32
}
function foo() {
  return this.a;
}
console.log(foo.simBind(obj)()); // yes !!! we can get a 32

// second time to solve the first time function cannot introduct arguments
Function.prototype.simBind = function(context) {
  const self = this;
  let arg1 = Array.prototype.slice.call(arguments, 1)
  return function() {
    let argArray = Array.prototype.slice.apply(arguments);
    return self.apply(context, arg1.concat(argArray))
  }
}

function foo(n1, n2) {
  return this.a + n1 + n2;
}
console.log(foo.simBind(obj, 11)(12)); // yes !!! we can get a 55
console.log(foo.simBind(obj, 11, 12)()); // yes !!! we can get a 55


// now we should deal the new function `this` point 
// in the bind function when we new is `this` is not ponit the thisArg.

var value = 1;
var foo = {
  value: 2
}
function bar (name, age) {
  this.habit = 'sleep';
  console.log(this.value);
  console.log(name)
  console.log(age)
}

bar.prototype.friend = 'zero'

// =====bind resulte====
var bindFoo = bar.bind(foo, 'myname');

var obj = new bindFoo(12);
// now `this` is point obj so  console.log(this.value) is undefined
// myname
// 12

console.log(obj.habit) // sleep
console.log(obj.friend) // zero

// =====simBind resulte====
var simbindFoo = bar.simBind(foo, 'myname');

var obj2 = new simbindFoo(12); // this is also point simbindFoo
// 2
// myname
// 12

console.log(obj2.habit) // undefined
console.log(obj2.friend) // undefined

// and now the bind is different with my simBind is new Function `this` point is not a same object

// thrid time
Function.prototype.simBind = function(context) {
  const self = this;
  let arg1 = Array.prototype.slice.call(arguments, 1)

  var fonp = function() {}
  var found =  function() {
    let argArray = Array.prototype.slice.apply(arguments);
    return self.apply(this instanceof fonp ? this : context, arg1.concat(argArray))
  }
  fonp.prototype = this.prototype;
  found.prototype = new fonp();
  return found;
}
// end the simBind.....
```

** refrence doc **
> [MDN call](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/call)
> [MDN apply](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
> [MDN bind](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
> [lvan sifrim](https://medium.com/@ivansifrim/the-differences-between-call-apply-bind-276724bb825b)
> [niladri sekhar dutta](https://www.codementor.io/niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)
> [mqyqingfeng](https://github.com/mqyqingfeng/Blog/issues/11)