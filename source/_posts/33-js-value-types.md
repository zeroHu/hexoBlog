---
title: 33-js-value-types
date: 2019-05-29 09:45:45
tags: 33-js-concepts
keywords: primitive types, value types, reference types, js值类型
---
### the primitve values and the reference values
* Primitive types are stored by value, objects are stored by reference

#### primitive values

> the ECMAScript define the values has [boolean, null, undefined, number, string,  symbol(es6 add)]

* the primitive values stored on the stack
* primitive types are no methods attached to them and the primitive values are immutable, because the have no methods attached that can mutate it
* the booleans value is true or false
* the number values is double-precision 64-bit float. there are no integers in js

```javascript
// to explain the stored in the stack 
var name = "zero"
console.log(name); // zero

var secondName = name;
console.log(secondName); // zero

name = 'chris';
console.log(secondName); // zero
console.log(name); // chris
```

```javascript
//  to explain the primitive types are immutable
"dog" === "dog"; // true
14 === 14; true


{} === {} // false
[] === [] // false
(function () {}) === (function () {}) // false
```



#### reference values
> [object], and the Array also is object.

* the reference value stored on the heap
* a function is a special type of object. with some special properties. such as constructor and call

```javascript
var person = {
  age: 20,
  name: 'zero'.
  hobbies: ['sports', 'cooking']
}
console.log(person); 
// [object Object] {
//   age: 20,
//   name: 'zero'.
//   hobbies: ['sports', 'cooking']
// }

var secondPerson = person;
console.log(secondPerson); 
// [object Object] {
//   age: 20,
//   name: 'zero'.
//   hobbies: ['sports', 'cooking']
// }

person.name = 'chris';
console.log(person);
// [object Object] {
//   age: 20,
//   name: 'chris'.
//   hobbies: ['sports', 'cooking']
// }
console.log(secondPerson);
// [object Object] {
//   age: 20,
//   name: 'chris'.
//   hobbies: ['sports', 'cooking']
// }
```
 
** the stack is different with heap place in the memory , the stack value is very fast to get or set. and the heap is longer than stack **

