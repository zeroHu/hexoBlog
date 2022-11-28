---
title: 33-js-expression-statement
date: 2019-06-09 16:38:24
tags: 33-js-concepts
keywords: steatement, expression, 表达式, 声明, 函数表达式, 函数声明
---
> javascript has two methods create functions, function expression and function declaration

```javascript
function funDeclaration() {
    return 'a function declaration'
}
var funExpression = function() {
    return 'a function expression'
}
```
**different with function declarations and function expressions**
* similar to the `var`, the function declaration are hosited at the top of other code. and the function expression not.
### function declarations
> a function declaration defineds a named function variable without requiring variable assignment. function declarations occur as standalone constructs and connot be nested within non-function blocks.

```javascript
alert(bar()) // 3 right!!!
function bar() {
    return 3
}
bar() // 3
bar // function
```

### function expressions
> a function expression defined a function as a part of a larger expression syntax.

```javascript
alert(bar()) ; // typeerror 
var bar = function () {
    return 3
}
(function IIFE() {
    alert('something');
})()
```
### Benefits of Function Expressions
* as a clousures
* as arguments to other functions
* as immediately invoked function expressions (IIFE)

```javascript
// creating closures
function toHandle1(index) {
    return function tabClickEvent(evt) {
        // do something
    }
}
var toHandle2 = function (index) {
    return function tabClickEvent(evt) {
        // do something
    }
}
var tabs = document.querySelectorAll('.tab')
for (let i=0; i<tab.length; i++) {
    tabs[i].onclick = toHandle1 // good code
    tabs[i].onclick = toHandle2 // bad code
}

//passing as a arguments
$(document).ready(function() {
    // do something
}) 
[1, 2, 3].forEach(function doSomething() {
    // do somthing
})

// IIFE
var module = (function() {
    var someMethod = function() {
        // also do something
    }
    return {
        someMethod: someMethod
    }
})()
```

**refrence doc**
> [Paul Wilkins](https://www.sitepoint.com/function-expressions-vs-declarations/)
