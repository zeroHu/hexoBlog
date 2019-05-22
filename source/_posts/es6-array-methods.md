---
title: Why and when to use forEach, map, filter, reduce, and find in JavaScript
date: 2019-05-07 15:03:45
tags: ES6
keywords: es6 array常用方法， forEach，es6，map，reduce，filter
---
### Maybe change use for in anywhere is better
#### forEach

> As well known that forEach is a way to work with items in array, anytime when i what loop a array, then first time i will think about forEach... i am so sad !!!

```javascript
// for loop
var arr = ['a', 'b', 'c']
for (let i=0; i<arr.length; i++) {
  console.log(arr[i])
}

// forEach loop
arr.forEach((item, index, array) => {
  console.log('item-->', item, 'index-->', index, 'array-->', array);
})

// compare the for and forEach
// for loop define a variable i, and set add ++ , ant the forEach loop you can do nothing
```

#### map

> As well known that forEach is generic tool in array loop, and when should we use map.
  how does map work ?
  map basically it takes 2 arguments(callback, thisArg), a callback and a optional context(will be considered as this in the callback) . and the callback runs for each value in the array and returns each new value in the 
  resulting array

  the callback function takes 3 arguments (currentValue, indexNumber, array)

```javascript
var arr = [{
  id: 1, value: 'a'
}, {
  id: 2, value: 'b'
}]
// if you want ['a', 'b'], you can use map now!!!
var newArr = arr.map(item => item.value) // so easy

// of cause you can use forEach or for or for..in and so on. but i think the map is you best choice
// example forEach
var newArr = []
arr.forEach(item => {
  newArr.push(item.value)
});
```

#### reduce

> ok, reduce just like map, also takes 2 arguments(callback, initialValue), and the callback is for each element of array, the initialValue is the first use callback first arguments value, if no initialValue will be the array first value. totally reduce is an easy way to generate a single value or object from an array.
  the callback function takes 4 arguments [Accumulator (acc) (累计器), Current Value (cur) (当前值), Current Index (idx) (当前索引), Source Array (src) (源数组)]

```javascript
// if we want to know total number of array some key add or the biggest one or the smallest. what time you should use reduce
var arr = [{
  year: 10,
  name: 'jane'
}, {
  year: 12,
  name: 'jake'
}]

// totalNumber example
var totalYears = arr.reduce((accumulator, item) => {
  return accumulator+item.year
}, 0)

// biggest example
var biggest = arr.reduce((acc, item) => {
  return (acc.year || 0) > item.year ? acc : item
}, {})

// smallest example
var smallest = arr.reduce((acc, item) => {
  return acc.year > item.year ? item : acc
}, arr[0])
```


#### filter
> this methods is easy, filter just filter a value in array, such as you want the array name === luce , what time you should use filter

```javascript
// if you want to name === jake 

var arr = [{
  year: 10,
  name: 'jane'
}, {
  year: 12,
  name: 'luce'
}]
var luceArray = arr.filter(item => item.name === 'luce');
```

tips:*渣渣英文，渣渣翻译，自己能看懂就不错了...望有待提高中*

**参考文档**
[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)
[poka-techblog](https://medium.com/poka-techblog/simplify-your-javascript-use-map-reduce-and-filter-bd02c593cc2d)

