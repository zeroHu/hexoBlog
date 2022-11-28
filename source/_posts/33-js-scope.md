---
title: 33-js-scope
date: 2019-06-04 17:32:01
tags: 33-js-concepts
keywords: js 函数作用域， 块作用域，词法作用域，scope, function scope, block scope, lexical scope
---
### scope
#### function scope
##### function basic info
* function is a subprogram designed to perform a particular task.
* function is executed when they are called. this is known as invoking a function
* values can be passed in function and used within the function
* functions always return a value, in js if function no `return` code, in fact the function return `undefined` see the example 1
* function are objects
* function scope use variable is cannot use in out of the function

example 1
```javascript
function testNoReturn() {
  var a = 1;
  var b = 1 + a;
}
function testHasReturn() {
  var a = 1;
  var b = 1 + a;
  return b
}
console.log(testNoReturn()); // undefined
console.log(testHasReturn()); // 2
console.log(a) // ReferenceError: a is not defined
```
##### define function and function expression and scope
> a function declaration defines a named function. to create a function declaration you use the `function` keyword followed by the name of the function.
> a function expressions defines a named or anonymous function. and they cannot be used before they are defined.
> use `var` or `let` or `const` declared a variable in the function , meaning it will exist within the scope of the function it's declared inside of.

```javascript
// you can in here called the name function . `name()`
console.log(a) // ReferenceError: a is not defined because a is not defined in out of the name function scope
function name(parameters) {
  var a = 'a'
}
// scope explain
console.log(a) // ReferenceError: a is not defined because a is not defined in out of the name function scope
// you cannot in here called the name function, will throw error
console.log(b) // ReferenceError: b is not defined because a is not defined in out of the name function scope
let name = function(parameters) {
  var b = 'b'
}
console.log(b) // ReferenceError: b is not defined because a is not defined in out of the name function scope
// you only can in here called the name function
```
#### block scope `let` and `const`
> block scope is the {} scope. but `var` is different with `let` or `const`

```javascript
console.log(name); // zero
console.log(sex); // ReferenceError: sex is not defined
if (true) {
  var name = 'zero';
  let sex = 'woman'; // const is same as let
}
console.log(name); // zero
console.log(sex); // ReferenceError: sex is not defined

// when function scope gets confusing with global scope

var hobbies = 'sleep'
const func = () => {
  var hobbies = 'play';
  console.log(hobbies); // play
}
func();
console.log(hobbies); // sleep

// when var in block scope
var hobbies = 'sleep';
if (true) {
  var hobbies = 'play'; 
  console.log(hobbies); // play
}
console.log(hobbies); // play
// because the hobbies play will cover the hobbies sleep
// but when you use let is different with var, the result same as the function scope. certainly explain that the block scope
```
#### lexical scope
```javascript
var value = 1
function foo() {
  console.log(value); // 1
}
function bar(){
  var value = 2
  foo()
}
bar();
```

**reference doc**
> [brandon Morelli](https://codeburst.io/javascript-functions-understanding-the-basics-207dbf42ed99)
> [deadcoderising](https://www.deadcoderising.com/2017-04-11-es6-var-let-and-const-the-battle-between-function-scope-and-block-scope/)
> [you dont't know javascript](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/ch3.md)
