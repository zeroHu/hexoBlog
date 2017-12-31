---
title: es6-set-map
date: 2017-12-31 20:24:01
tags: ES6
---
### Set
> es6 提供了新的数据结构Set,它类似于数组，但是成员是唯一的，没有重复的值。
Set本身是一个构造函数，用来生成Set数据结构
```javascript
const s = new Set()
[2, 3, 4, 5, 2, 2].forEach(x => s.add(x))
s // [2, 3, 4, 5]
```
上面的结果表明Set结构不会添加重复的值。Set函数可以接受一个数组作为参数，用来初始化。
```javascript
    // 例1
    const set = new Set([1, 2, 3, 4, 4])
    [...set] //[1, 2, 3, 4]
    // 例2
    const items = new Set([1, 2, 3, 4, 5, 5, 5, 5])
    items.size //5
    // 例3
    function divs() {
        return [...document.querySelectorAll('div')]
    }
    const set = new Set(divs())
    set.size //56
    // 类似于
    divs().forEach(div => set.add(div))
    set.size
```
去除数组重复成员
```javascript
[...new Set(array)]
//向Set加入值得时候不会发生类型转换，所以 5 和 ‘5’是两个不同的值，Set内部判断两个值是否相同，使用的算法是“some-value equality" 它类似的值精确等于 === 主要的区别是NaN 等于自身
```
#### Set实例的属性和方法
set的结构的实例有以下属性
> Set.prototype.constructor:构造函数，默认是Set的函数
  Set.prototyep.size 返回Set实例成员的个数

Set实例的方法分为两大类：操作方法（操作数据）和遍历方法（用于遍历成员）
> add(value) 添加某个值，返回Set结构本身
  delete(value) 删除某个值，返回一个布尔值，表示删除成功
  has(value) 返回一个布尔值，表示该value是Set的成员
  clear() 清除所有成员，没有返回值

#### Array.from 可以将 Set数据类型转为数组
```javascript
    const items = new Set([1, 2, 3, 4, 4])
    const array = Array.from(items)
```
#### 遍历操作
Set 结构的实例有四个遍历方法，可以用于遍历成员
> keys() 返回键名的遍历器
  values() 返回键值得遍历器
  entries() 返回键值对的遍历器
  forEach() 使用回调函数遍历每个成员

Set结构没有键名，只有键值（或者说键名和键值是同一个值）所以keys() 和 values()方法完全一样
```javascript
    let set = new Set(['red', 'green', 'yellow'])
    for (let item of set.keys()) {
        console.log(item);
    }
    //'res' 'green' 'yellow'

    let set = new Set(['red', 'green', 'yellow'])
    for (let item of set.values()) {
        console.log(item);
    }
    //'res' 'green' 'yellow'

    let set = new Set(['red', 'green', 'yellow'])
    for (let item of set.entries()) {
        console.log(item);
    }
    //['res','res']  ['green','green']   ['yellow','yellow']
```
Set结构默认是可遍历的 默认是values方法，也就是可以省略values方法直接用for 循环
```javascript
    let set = new Set(['red', 'green', 'yellow'])
    for(let i of set){
        console.log(i)
    }
    // 同样的 Set结构也是有 forEach方法 对于每个成员进行操作，没有返回值
    set = new Set([1,4,9])
    set.forEach((value, key) => {console.log(key + '-' + value)})
```
### Map
#### 含义和基本用法
> javascript 对象，本质上是键值对的集合（hash结构），但是传统上只能用字符串这个它的使用带来了很大的限制
```javascript
    const data = {}
    const element = documetn.getElementById('myDiv')
    data[element] = 'metadata'
    data['[object HTMLDivElement]'] //metadata
    // 这段代码的原意是将一个DOM节点作为data的键，但是对象只接受字符串作为键名，所以element被自动转为字符串【object HTMLDivElement】
```
Es6提供了Map结构，它类似于对象，也是键值对的结合，但是键不止于字符串，各种类型的值（包括对象）都可以当做键。也就是说Object提供”字符串一值“的对应，Map结构提供了”值-值“的对应，是一种更加完善的Hash结构的实现。
```javascript
    const m = new Map()
    const o = {p:'hello wold'}
    // 方法
    m.set(o,'content')
    m.get(0) // 'content'
    m.has(o) // true
    m.delete(o) // true
    m.has(o) // false
```
作为构造函数 Map也接受一个数组作为参数，该数组的成员是一个个表示键值对的数组

```javascript
    const map = new Map([
        ['name', 'zero],
        ['title', 'author']
    ])
    map.size // 2
    map.get(name) //zero
    map.has(name) //true
```