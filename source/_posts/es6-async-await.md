---
title: es6-async-await
date: 2017-12-20 16:41:01
tags: ES6
keywords: es6 async, es6, await, async await，gennerator
---
### async
> 通俗的来讲 gennerator 的语法糖

#### 初步了解
先回忆一下 gennerator

```javascript
const fs = require('fs');

const readFile = function (fileName) {
    return new Promise(function (reslove, rejecrt) {
        fs.readFile(fileName, function(error, data) {
            if (error) return reject(error);
            resolve(data)
        })
    })
}
const gen = function* (){
    const f1 = yield readFile('/etc/fstab')
    const f2 = yield readFile('/etc/shells')
    console.log(f1.toString())
    console.log(f2.toString())
}

//调用的时候是

gen.next()
gen.next()

```
将上面的gennerator 函数转化为 async 函数就是
```javascript
const asyncReadFile = aysnc function () {
    const f1 = await readFile('/etc/fstab')
    const f2 = await readFile('/etc/shells')
    console.log(f1.toString())
    console.log(f2.toString())
}
//调用的时候
asyncReadFile()
```
区别点
> generator 函数执行必须靠执行器，所以有了co模块，而async 函数自带执行器，也就是async函数执行和普通函数一样
  更好的语义
  更适用的广泛性
  返回的是promise

#### 基本用法
> async 返回一个promise对象，可以使用then方法添加回调函数。当函数执行的时候一旦遇到await就会先返回，等到异步操作完成。再接着执行函数体后面的语句。

example
```javascript
// first example
async function getStorePriceByName (name) {
    const symbol = await getStockSymbol(name)
    const stockPrice = await getStockPrice(symbol)
    return stockPrice
}
getStorePriceByName('goog').then(function (result) {
    console.log(result)
})

// second example
function timeout (ms) {
    return new Primise((resolve) => {
        setTimeout(resolve,ms)
    })
}
async function asyncPrint (value, ms) {
    await timeout(ms)
    console.log(value)
}
asyncPrint('hello', 3000)
```

#### async 函数的多种使用形式
```javascript
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {}

// 对象的方法
let obj = {
    async foo() {}
}

// class 的方法
class Storage {
    constructor() {
        this.cachePromise = cache.open('avatars')
    }
    async getAvatar(name) {
        const cache = await this.cachePromise
        return cache.match(`/avatars/${name}.jpg`)
    }
}

const storage = new Storage()
storage.getAvatar('zero').then(..)

// 箭头函数
const foo = async () => {}
```
#### 语法
> 返回promise对象，async函数内部return语句返回的值，会成为then方法回调函数的参数

```javascript
    async function f() {
        return 'hello world'
    }
    f().then(v => console.log(v))//'hello world'
    /*
    上面代码中函数f内部return命令返回的值，会被then方法回调函数接收到
    */
```
async 函数内部抛出错误，会导致返回的primise对象变为reject状态。抛出的错误对象会被catch方法函数接收到
```javascript
    async function f() {
        throw new Error('somethins is wrong')
    }
    f().then(
        v => console.log(v),
        e => console.log(e)
    )
    //Error: 出错了
```
### await命令
> 正常情况下 await命令后面是一个Promise 对象。如果不是，会被立即转为一个resolve的promised对象

```javascript
async function f() {
    return await 123
}
f().then(v => console.log(v))//123
/*
    上面代码中，await命令参数是数值123，它被转为promise对象。并立即执行resolve中
    await 命令的promise对象如果变为reject 状态。则reject的参数会被catch 方法的回调函数接收到
*/

async function f2() {
    return Promise.reject('it is wrong')
}
f().then(
    v => console.log(v),
    e => console.log(e)
)
//it is wrong
```
#### 使用注意点
> 1.await 命令后面的promise对象，运行的结果可能是rejected。所以最好把await命令放在try ... catch中

```javascript
    async function myFunction() {
        try {
            await somethingRunInPromise()
        } catch (err) {
            console.log(err)
        }
    }
    //或者
    async function myFunction() {
        await somethingRunInPromise()
        .catch(function (err) {
            console.log(err)
        })
    }
```
> 2.多个await命令后面的异步操作，如果不存在继发关系，最好让它们同时触发

```javascript
    let foo = await getFoo()
    let bar = await getBar()
    /*
    上面的代码中，getFoo 和 getBar 是两个独立的异步操作(即互不依赖)，被写成继发的关系这样会比较耗时间，
    因为只有 getFoo 函数完成后才会 开始 getBar
    */
    // ====== 同时触发 ======
    // 写法一
    let [foo,bar] = await Promise.all([getFoo(), getBar()])
    // 写法二
    let foopromise = getFoo()
    let barpromise = getBar()
    let foo = await foopromise
    let bar = await barpromise
```
> 3.await 只能用于 async 函数中。并且forEach 函数中不适合用async 函数 ，如有需求，改为for循环

#### async函数的实现原理
> async 函数的实现原理，就是讲generator函数和自动执行器，包装在一个函数里面

#### 实例(按照顺序完成异步操作)
```javascript
    function logInOrder(urls) {
        // 远程读取所有的url
        const textPromises = urls.map(url => {
            return fetch(url).then(response => response.text())
        })

        // 按次序输出
        textPromises.reduce((chain, textPromise) => {
            return chain.then(() => textPromise)
                        .then(text => console.log(text))
        }, Promise.resolve())

        // 改为async
        async function logInOrder2(urls) {
            // 并发处理
            const textPromises = urls.map(async url => {
                const response = await fetch(url)
                return response.text()
            })
            // 按次序输出
            for (const textPromise of textPromises) {
                console.log(await textPromise)
            }
        }
    }
```

