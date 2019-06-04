---
title: 33-js-closures
date: 2019-05-13 14:45:53
tags: 33-js-concepts
keywords: closures, 闭包
---
### closures
first we should know closures is what ?
> the MDN explain that a closure is the combination of a function and the lexical environment within which that function was declared. and i'm sure that you have use closure in your code everywhere. maybe you don't know that but it's obvious.

#### a function that returns a function
```javascript
function createAdder () {
  let counter = 0;
  function addNumbers () {
    counter = counter + 1;
    return counter;
  }
  return addNumbers;
}
let adder = createAdder();
let c1 = adder(); // 1
let c2 = adder(); // 2
let c3 = adder(); // 3
console.log(c1, c2, c3);

// when you declare a new function and assign it to a variable, you store the function definition, as well as a closure.
// the closure contains all the variables that in scope at the time of creation of the function.
// it is analogous to a backpack. a function definition comes with a little backpack. and in its pack it stores all the 
// variables that were in scope at the time that the function definition was created.

// ***so let's explain how it works the top code***

// 1. lines 1-8, create a new variable createAdder in the global execution context and it gets assigned function definition. 
// 2. line 9, we declare a new variable named adder in the global execution context. 
// 3. line 9 again, we call the createAdder function and assign its returned value to the adder variable.
// 4. lines 1-8 calling the function. greating new local execution context.
// 5. line 2. within the local execution context, declare a new variable named counter . number 0 is assigned to counter.
// 6. lines 3-6 .declare new variable named addNumbers. the variable is declared in the local execution context. the content of the variable is yet another function definition. as
// defined in lines 4 and 5. now we also crate a closure and include it part of the function definition. the closure contains the variables that are in scope. in this case the variable counter
// 7. line 7, returning the content of the addNumbers variable. local execution context is deleted. addNumbers and counter no longer exist. 
// control is returned to the calling context. so we are returning the function definition and its closure.the backpack with the variables that were in scope when it was created.
// 8. line 9 . in the calling context, the global execution context, the value returned by createAdder is assigned to adder, the variable adder now contains a function definition(and closure). 
// the function definition that was returned by createAdder. it is no longer labeled addNumbers, but it is the same definition. within the global context, it is called adder.
// 9. line 10, declare c1
// 10. line 10 again, look up the variable adder, it's function, call it. it contains the function definition returned from earlier, as defined in line 4-5(and it also has a backpack with variables)
// 11. create a new execution context, there are no parameters. start execution the function
// 12. line 4, counter = counter + 1, we need to look foor the variable counter, before we look in the local or global execution context, let's look in our backpack.
// let's check the closure. lo and behold. the closure contains a variable named counter with a value of 1
// 13. line 5, we return the content of counter. or the number 1, we destory the local execution context
// 14. back to the line 10, the returned value 1 gets assigned to c1. 
// 15. the c2 and c3 is same to c1 but the backpack counter is add and store .so the c2 is 2 and the c3 is 3.
```
**the closure is a collection of all the variables in scope at the time of createion of the function**

**reference doc**
> [dailyjs](https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8)
> [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
> [jsinfo](https://zh.javascript.info/closure)