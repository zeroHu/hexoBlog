---
title: 33-js-iife-module-namespace
date: 2019-06-09 19:20:12
tags: 33-js-concepts
---
### anonymous function expressions and named function expressions
```javascript
var bar = function () {
    return "you are good"
}
// this bar variable assign function is a anonymous function
var bar  = function bar() {
    return "you aslo good"
}
// the function bar is a named function exrepisons
```

### iife(inmediately-invoking-function-expression)
natural function definition
```javascript
// function declaration
function foo() {
    return "hello zero"
}
foo()
// the line 2-5 is define a function named foo
// the line 6 is add () to called the foo function
// function expression
var bar = function() {
    return "hello zero"
}
bar();
// the line 9-11 is declare a variable var and assign a value to that's of function type
// the line 12 is called the function
```
iife
```javascript
!function() {
    console.log('ok!');
}(); // ok!
void function() {
    console.log("void");
}()
```
* as we know that a function statement has keyword `function`
* `!`in front of function , that enfores javascript to treat whatever that's coming after `!` as an expressions
* and the last `()` is immediately called the function
* `+`, `-`， `~`, `void` is the same to `!` in font of function

classical iife style
```javascript
(function() {
    var a = 1
    console.log("classical 1");
})();

(function() {
    var b = 2
    console.log("classical 2");
}())
a // error
b // error
```
IIFE and private variables
> the iife is good to do that their ability to create a function scope, any variable is defined in the iife function are not visible to outside

IIFE with return value
```javascript
var needVariable = (function(){
    return "hello world"
}())
console.log(needVariable);// hello world
```
IIFE with parameters
```javascript
(function IIFE($, window, docuemnt, undefined) {
    console.log($, window, docuemnt, undefined);
})(jQuery, window, document)
```


**reference doc**
> [Chandra Gundamaraju](https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6)

