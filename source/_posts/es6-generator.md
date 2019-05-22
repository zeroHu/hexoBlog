---
title: es6-generator
date: 2017-12-18 10:54:15
tags: ES6
keywords: es6 generator
---
### Generator函数
> generator 函数是es6提供的一种异步编程解决方案，语法行为与传统函数完全不同.generator 函数是一个状态机，封装了多个内部状态。执行generator函数会返回一个遍历器对象，也就是generator函数除了状态机，还是一个遍历器对象生成函数，返回的遍历器对象，可以一次遍历generator函数内部的每一个状态

> generator 函数与不同函数不同的特征。
  * function关键字与函数名之前有一个星号
  * 函数体内部使用yield表达式

```javascript
function* helloWroldGenerator(){
    yield 'hello';
    yield 'world';
    return 'ending';
}
var hw = helloWroldGenerator();
```

generator 函数的调用方法与普通函数是一样的，也是在函数后面加上一对圆括号。不同的是，调用generator 函数后，该函数并不执行，返回的也不是函数运行结果。而是一个指向内部状态的指针对象。下一步，必须调用遍历器对象的next方法，使得指针移向下一个状态。也就是说，每次调用next方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个yield表达式（或return语句）为止。换言之，Generator 函数是分段执行的，yield表达式是暂停执行的标记，而next方法可以恢复执行。


```javascript
hw.next()
//{value:'hello',done:false}
hw.next()
//{value:'world',done:false}
hw.next()
//{value:'ending',done:true}
hw.next()

```
### yield 表达式
> 由于generator 函数返回的遍历器对象，只有调用next方法才会遍历下一个内部状态，所以其实提供了一种可以暂停执行的函数，yield表达式就是暂停标志。
遍历器对象的next方法的运行逻辑如下。

> 遍历器对象的next方法运行逻辑如下.
 1）遇到 yield 表达式，就展厅执行后面的操作，饼将紧跟在yield后面的那个表达式的值，作为返回的对象的value属性值
 2）下一次调用next方法时，再继续往下执行，知道遇到下一个yield表达式
 3）如果没有再遇到新的yield表达式，就一直运行到函数结束，知道遇到return语句位置，并将return语句后面的表达式的值，作为返回的对象的value属性值
 4)如果该函数没有 return语句，则分会的对象的value属性值为undefined

** 另外需要注意，yield表达式只能用在 Generator 函数里面，用在其他地方都会报错。 **








