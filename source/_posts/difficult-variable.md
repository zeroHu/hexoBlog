---
title: js 传值方式
date: 2018-04-13 11:29:13
tags: js 困惑
---
### 挖掘js 传值方式
#### 值的存储方式 （[图的来源](https://yangbo5207.github.io/wutongluo/ji-chu-jin-jie-xi-lie/yi-3001-nei-cun-kong-jian-xiang-jie.html))
![变量的存储](http://upload-images.jianshu.io/upload_images/599584-8e93616d7afcf811.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 几个小栗子
```javascript
// 基本类型
var x = 1;
function test(m) {
    m = 2
}
test(x);
console.log(x); // 1

// 对象
var obj = {
    a: 1
}
function test(m) {
    m.a = 2
}
test(obj);
console.log(obj); // {a:1}

// 依旧是对象
var obj = {
    a: 1
}
function test(m) {
    m = 2
}
test(obj);
console.log(obj); // {a:1}     ??? what mmp
```
what??? 这👆的结果简直让人困惑，不知道 js 到底是按照值传递还是按照引用传递。
#### <font color="red">共享传递</font>
* 1.js中基本类型按照值传递
* 2.对象类型按照*共享传递*
> 共享传参理解是：调用函数传参时，函数接受对象实参引用的副本。

```javascript
var obj = {
    a: 1
}
function test(m) {
    // 这里的m 是相当于创建了一个副本obj，引用相同的值，同时也解释了为啥改内部值可以，但是重新复制就相当于重新换了一个指向
    m.a = 2
}
test(obj);

```

#### 个人总结：要修改一个非对象内的某个值的时候，不要使用函数传参
#### 原文地址
> [原文](http://bosn.me/js/js-call-by-sharing/)
