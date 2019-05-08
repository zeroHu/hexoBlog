---
title: 33-js-recursion
date: 2019-05-08 11:18:50
tags: 33-js-concepts
---

### recursion(递归)

> explain ： recursion is simply when a function calls itself

#### factorial example
```javascript
// this function use recursion
function factorial (n) {
  if (n < 0) {
    return;
  }
  else if (n === 1) {
    return 1;
  }
  else {
    return n * factorial(n-1); // the most important line
  }
}
factorial(4) // 4*3*2*1

// and the compute is
// factorial(4)
//   4 * factorial(3)
//     3 * factorial(2)
//       2 * factorial(1)
//         1
//       resuming previous execution 2 * 1 = 2
//     resuming.. 3 * 2 = 6
//   resuming.. 4 * 6 = 24
// factorial(4) = 24
```

#### the three key features of recursion
> `if (something bad happened) { STOP }` this is the safe condition. otherwise will error happen
   such as the factorial `if (n< 0) { return }` just stop the unbelieveble loop 

----
> `if (this happens) { yay! you should done }l` this is the done the loop.
  such as the factorial `if (n===1) { return }` just stop the loop

----
> `return n * factorial(n-1)` is the recursion!!!


### tail calls(尾调用)
> the tail calls is `function f(x) { return g(x) }` not `function f(x) { return g(x) + 1 }`. means return a function and don't need compute again

#### factorial example
```javascript
function factorial(n, res) {
  if (n === 1){
    return res
  }
  return factorial(n-1, res * n);
}
factorial(4, 1);
// and the compute is
// factorial(4, 1)
//   innter anonymous function (iaf) get called with (n=4, res=1)
//   iaf(3, 3*4)
//     iaf(2, 2*12)
//       iaf(1, 24)
//         24
//       24
//     24
// factorial(4, 1) = 24
```

> summarize : the tail call in stack is less, in v8 can spend less time

![](http://static.zeroyh.cn/33-WechatIMG734.png)