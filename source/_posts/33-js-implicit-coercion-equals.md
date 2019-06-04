---
title: 33-js-implicit-coercion-equals
date: 2019-06-04 12:25:48
tags: 33-js-concepts
keywords: js数据类型强制转换，===vs==
---
### implicit coercion
```javascript
// when you want to  these operators -, *, /, %
// 强制转换字符型为数字型
3 + "3" // 6 
2 * "2" // 4
// boolean 在计算中被强制转换为 true => 1, false => 0
true + true // 2
10 - true // 9
// object 被转为 object.valueOf, 如果没有valueOf则会取toString
const foo = {
  valueOf: () => 2
}
3 + foo // 5
const bar = {
  a: () => 2
}
3 + bar // 3[object Object]

const other = {
  toString: () => ' promise is a string'
}
3 + other // 3 promise is a string
// and when the toString and valueOf all in, the compute will choose which ?
const both = {
  valueOf: () => 2,
  toString: () => 'ok i am the both toString'
}
3 * both // 6
// 数组参与计算同样会被 toString() [].toString = "" 
4 * [] // 0
4 * [2] // 8
4 + [2] // 42
4 + [1,2] // 41,2
4 * [1, 2] // NaN
// 字符会被强制转为boolean false or true, null, undefined, 0, "", NaN 会被强制转为false
'string' ? 4 : 1 // 4
undefined ? 4 : 1 // 1
```
非数值类型的在数值计算中的表现
#### String
```javascript
3 * "3" // 3 * 3
3 * Number("3") // 3 * 3

Number("1.") // 1
Number("1.34") // 1.34

Number("1,") // NaN
Number("1+1") // NaN
Number("one") // NaN
```
#### Object
```javascript
"name" + {} // name[object Object]
```
#### Array
```javascript
[1,2,3].toString() // 1,2,3
// just as join()
[1,2,3].join() // 1,2,3
```
#### Boolean
```javascript
Number(true) // 1
Number(false) // 0
Number("") // 0
```
#### falsy and truthy
> falsy: false, 0, null, undefined, "", NaN, -0. and the other is truthy

#### NaN
```javascript
NaN === NaN // false
const notNumber = 3 * "a" // NaN
notNumber == notNumber // false
notNumber === notNumber
```
### == vs ===
> == 和 === 区别是 === 是禁止运算类型转换的，而==是支持的！

```javascript
// 先看一组热闹
5 === 5 // true
"hello world" === "hello world" // true
true === true // true
false === false // true
// 几个小特殊
{} === {} // false
[] === [] // false
NaN === NaN // false
(function(){}) === (function(){}) // false
// 再看一组热闹
7 === '7' // false
7 == '7' // true
false === 0 // false (different type and different value)
false == 0 // true
false == '0' // true 
false == '' // true
0 == "" // true
'cat' === 'dog' // false
```
#### why {} === {} or [] === [] is false
> 因为 {} 和  [] 是reference types(引用类型数据)， 引用 类型数据比较的是地址。而不是值。

```javascript
var a = {}
var b = {}
a == b // false
a === b // false
var c = a
c === a // true
c == a // true
c === b // false
c == b // false
// 证明了上面的结论， 作为引用类型数值，在== or === 比较的时候比较的是引用的地址而不是值
```
#### null === vs == undefined
```javascript
null == null // true
null === null // true
null == undefined // true
null === undefined // false
```
#### NaN is not equal any value
```javascript
NaN == null // false
NaN == undefined // false
NaN == NaN // false
// we can use isNaN test the value is NaN 
```
**reference doc**
> [brandon morelli](https://codeburst.io/javascript-double-equals-vs-triple-equals-61d4ce5a121a)
> [promise tochi](https://dev.to/promhize/what-you-need-to-know-about-javascripts-implicit-coercion-e23)
