---
title: es6-standard(es6 标准)
date: 2017-06-30 15:36:47
tags: ES6
---
前言：
> 了解了一些es6的用法，但是一直没有系统的看关于es6的所有改变，于是这次看[**阮一峰老师的ES6标准入门**](http://www.ruanyifeng.com/blog/2017/09/es6_primer_3rd_edition.html)，记录下来方便自己查询。

-----
### 第一章：介绍了babel 如何将es6 转为 所有浏览器都识别的es5
> .babelrc

```javascript
{
	"presets":[
		"es2015",
		"stage-2"
	],
	"plugins":[]
}
```
> package

```javascript
{
    "name": "es6Demo",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "build": "babel src -d lib"
    },
    "repository": {
        "type": "git",
        "url": "git+https://github.com/zeroHu/es6Demo.git"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "bugs": {
        "url": "https://github.com/zeroHu/es6Demo/issues"
    },
    "homepage": "https://github.com/zeroHu/es6Demo#readme",
    "devDependencies": {
        "babel-cli": "^6.24.1",
        "babel-preset-es2015": "^6.24.1",
        "babel-preset-stage-2": "^6.24.1"
    }
}
```
-----
### 第二章：let和const
#### let基本用法
> 1.let命令所在的代码块内有效，<br>2.let不允许声明重复的变量，<br>3.let不会存在变量提升(如果在声明前使用会报错)

```javascript
{
    let a = 0;
    var b = 1;
}
a //ReferenceErr
b //1
```
#### const基本用法
> const是声明一个只读的常量，也是代码块内

```javascript
if(true){
    const MAX = 5;
}
MAX // Uncaught ReferenceError
```
-----
### 第三章：数组的结构赋值
#### 3.1 为变量赋值
```javascript
//es5 声明变量的方式

var a = 1;
var b = 2;
var c = 3;
var sendA = [],
    sendB = [],
    sendC = [];

//es6 声明变量的方式

let [a,b,c] = [1,2,3];
let [sendA,sendB,sendC] = [[],[],[]];

//more example
let [head, ...tail] = [1, 2, 3, 4];
// head ==> 1
// tail ==> [2, 3, 4]
```
> 这种写法为模式匹配，只要等号两边相等就可以匹配,解构赋值不仅适用于var命令 , 解构不仅可以用于数组，还可以用于对象。，也适用于let和const命令。

```javascript
let [x,y,z] = new Set(["a","b","c"])
//x : a
```
#### 3.2 对象的解构赋值

```javascript
let {a,b} = { foo:"aa",bar:bb }
let { a = {}, b= {} } = {};
```

#### 3.3 字符的解构赋值
```javascript
    const [a,b,c,d,e] = 'hello';
    //a  'h'
    ...
    //e  'o'
```

#### 3.4 函数的解构
```javascript
    function add([x+y]){
        return x+y
    }
    add([1,2])//3
```
-----
### 第四章：字符串的拓展
#### includes(), startsWith(), endsWith()
* includes():返回布尔值，表示是否找到了参数字符串。
* startsWith():返回布尔值，表示参数字符串是否在源字符串的头部
* endsWith():返回布尔值，表示参数字符串是否在源字符串的尾部。

```javascript
var s = 'Hello world!';
s.startsWith('Hello')// true
s.endsWith('!') // true
s.includes('o') // true
```

#### repeat()
```javascript
let newarr = 'x'.repeat(10);//'xxxxxxxxxx'
```
#### 模板字符串"``"

```javascript
    let str = 'history';
    console.log(`this vue mode is ${str}`);//this vue mode is history
    const tmpl = addrs =>
        ` <table>
            ${addrs.map(addr => ` <tr><td>${addr.first}</td></tr> <tr><td>${addr.last}</td></tr>`).join('')}
        </table> `;
    const data = [
        { first: '<Jane>', last: 'Bond' }, { first: 'Lars', last: '<Croft>' },
    ];
    console.log(tmpl(data));
```
#### 模板编译实例
```javascript
let str = 'history';
console.log(`this vue mode is ${str}`);
const tmpl = addrs => ` <table>
    ${addrs.map(addr => ` <tr><td>${addr.first}</td></tr> <tr><td>${addr.last}</td></tr>
    `).join('')}
    </table> `;
const data = [
    { first: '<Jane>', last: 'Bond' }, { first: 'Lars', last: '<Croft>' },
];
console.log(tmpl(data));
```
#### 标签模板
> 是用来防止用户输入恶意代码

```javascript
    alert`hello`
    //等价于
    alert(hello)
    var a = 5; var b = 10;
    tag`Hello ${ a + b } world ${ a * b }`; // 等同于
    tag(['Hello ', ' world ', ''], 15, 50);
```
-----
### 第五章：数组的拓展
#### Array.from()
> Array是将两类对象转为真正的数组，类似数组的对象(array-like object)和可遍历(iterable)的对象(包括ES6新增的数据结构Set和 Map)

```javascript
    let arraylike = {
        'time':'12',
        'year':'13',
        'name':'zero'
    };
    let array = Array.from(arraylike);
    console.log(array); // []
```

#### 拓展运算符(...)也可以将某些数据结构转为数组
```javascript
// arguments对象
function foo() {
    var args = [...arguments];
}
// NodeList对象
[...document.querySelectorAll('div')]
```
#### 数组实例的includes()

```javascript
// includes 兼容性不太好
[1,2,34].includes(1);//true
['a','b','cd'].includes('f');//false
```

#### 数组的map filter
-----
### 第六章：箭头函数
```javascript
var f = f => f
//等同于
var f = function(f){
    return f;
}
```
> 去空，去重，排序函数

```javascript
const needPartKong = (arr) => Array.from(new Set(arr));//去重 1
let needarr = [1,2,3,2,1];
console.log(needPartKong(needarr));//[ 1, 2, 3 ]
console.log(needarr);//[ 1, 2, 3, 2, 1 ]

arr = [...new Set(arr)] //去重 2
```
> 如果箭头函数不需要参数或者需要多个参数的时候需要用（）包含

```javascript
var pagejson = {
    init(){
        //此处的this指向的并不是 $('.divone') 而是始终指向pagejson
        $('.divone').click(() => this.getData());
    },
    getData(){
        console.log('get data is ...');
    }
}
```
> 箭头函数的this指向是不会随绑定的对象而改变的而是定义的时候this的环境

-----
### 第七章：Object
#### Object.keys()
```javascript
    var json = { foo:"1",baz:"2" };
    Object.keys(json);//['foo','baz']
```
#### Object.values()
```javascript
    var json = { foo:"1",baz:"2" };
    Object.values(json);//['1','2']
```
#### Object.entries()
```javascript
    var json = { foo:"1",baz:"2" };
    Object.entries(json);//[['foo','1'],['baz','2']]
```