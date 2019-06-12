---
title: 33-js-pure-function
date: 2019-06-12 16:51:42
tags: 33-js-concepts
keywords: 纯函数, pure function
---
### what is a function
> a function is a process which takes some input, called arguments, and produces some output called a return value. functions may serve the following purposes:

* mapping: produce some output based on given inputs. a function maps input values to output values.
* procedures: a function may be called  to perform a sequence of steps. the sequence is known as a procedure, and programming in this style is known as procedural programming.
* I/O: some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network.

### pure functions are all about mapping
```javascript
Math.max(2,1,10,20) // 20
// in this example, 2, 1, 10, 20 are arguments. they're values passed into the function
```

### pure function
* 一个函数的返回结果只依赖于它的参数
* 在执行过程中里面没有副作用（表示不会更改外面的数据）
* 优点： 纯函数可靠性高，可读性高，bug率少。input一样的情况下output永远一样
```javascript
// 是纯函数
const add = (x, y) => x+y
const compute = x => {
  const obj = {a: 1}
  return x + obj.a
}
// 不是纯函数
const a = 1
const add = (x) => a + x // 依赖了a
const compute = (x, obj) => {
  return x + obj.a
}
compute(1, {a: 2}) 
```
