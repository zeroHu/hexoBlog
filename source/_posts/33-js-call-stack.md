---
title: 33-js-call-stack
date: 2019-05-14 17:03:27
tags: 33-js-concepts
keywords: call stack, 调用堆栈, js是如何执行的
---
### call stack

**what is call stack**
a call stack is a data structure that uses the last in, first out(IIFO) principle to temporarily store and manage function invocatin (call).

> call stack is tell us how is the function call, and just like a interpreter for mechanism. the order of function and what time is the function call , and what time is the function out.

#### why js is a single threaded single concurrent language
> as we know that javascript is a single threaded single concurrent language. but what's mean??? that means at a time js only can deal one task or a a piece of code. it has a single call stack which along with other parts like heap, queue constitutes the javascript concurrency modal.

![](http://static.zeroyh.cn/1_ZSFHnq9iMHIApVLcgwczPQ.png)

#### just to know how is js code run
* when a script calls a function, the interpreter adds it to the call stack.
* any function called by that function added to the call stack further up. and run anywhere their calls are reached.
* when the current function is finished. the interpreter takes it off the stack.
* if the stack takes more space than it had assigned, it results in a error "stack overflow".  

```javascript
function foo() {
    console.log('foo is start');
    return bar();
}
function bar() {
    console.log('bar is start');
}
console.log(foo());
// what's  the js running ? let me show you the call stack.
// 1. first when we run console.log(foo()); now the call stack will push the console.log(foo());
// 2. when foo() called, now call stack will push the foo()
// 3. then the foo called then return bar(), now call stack will push the bar()
// 4. now called bar, and run the `console.log('bar is start`) then the bar is pop off the call stack.
// 5. then the foo is pop off the call back
// 6. then the `console.log(foo())` is pop off the call stack
```
![the foo and bar run gif](http://static.zeroyh.cn/1_E3zTWtEOiDWw7d0n7Vp-mA.gif)
![the error show the call stack](http://static.zeroyh.cn/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%20%E4%B8%8B%E5%8D%8810.03.00.png)

**refrence doc**
> [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Call_stack)
> [Gaurav Pandvia](https://medium.com/@gaurav.pandvia/understanding-javascript-function-executions-tasks-event-loop-call-stack-more-part-1-5683dea1f5ec)
> [Vedio Philip Roberts](https://www.youtube.com/watch?v=8aGhZQkoFbQ&list=PL4SfyCkRAwT7LQmbaxcVWRTaQITtCCAwZ)