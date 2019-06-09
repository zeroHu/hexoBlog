---
title: 33-js-setTimeout-setInterval
date: 2019-06-09 22:17:00
tags: 33-js-concepts
keywords: setTimeout, setInterval, js定时器, 定时器, setTimeout 和 setInterval 区别
---
### setTimeout
> allows to run a function once after the interval time.

```javascript
let timerId = setTimeout(func | code, [delay], [arg1], [arg2], ...)
// func | code 指的是 函数名称或者直接写函数
function callBack(arg1, arg2) {
    // do something
}
// delay 是延迟多久执行
// arg1, arg2 是传递给回调函数的参数。
let timerId = setTimeout(callBack | function(arg1, arg2) {
    // do
}, 1000)

let timerId = setTimeout(callBack(), 1000) // the callBack function called right now, not 1s after
```
### clearTimeout
> a call to setTimeout returns a timer identifier , timerId can help us cancel the execution, and we can clearTimout(timerId) to cancel the execution.`clearTimeout(timerId)`

### setInterval
> allows to run a function regularly with the interval between the runs

```javascript
let timerId = setInterval(func | code, [delay], [arg1], [arg2], ...)
// func | code 指的是 函数名称或者直接写函数
function callBack(arg1, arg2) {
    // do something
}
// delay 是间隔多久执行一次
// arg1, arg2 是传递给回调函数的参数。
let timerId = setInterval(callBack | function(arg1, arg2) {
    // do
}, 1000)

let timerId = setInterval(callBack(), 1000) // the callBack function called right now, not 1s after
```
### clearInterval
> stop the further calls, use `clearInterval(timerId)`

### 用setTimeout 实现每隔一段时间执行某段代码
```javascript
let timerId = setTimeout(function tick() {
  console.log('tick');
  timerId = setTimeout(tick, 2000); // (*)
}, 2000);
// just 2s 执行一次 tick 函数，开始循环。 这种形式相对cpu耗用比 setInterval 少
```




