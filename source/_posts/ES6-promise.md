---
title: es6-promise
date: 2017-07-10 19:14:47
tags: ES6
---
### promise 理念
#### promise
> 一个promise 代表异步操作最终完成或者失败的对象，一个promise可以使用它的constructor创建。但是大多数使用的是其他函数创建并返回的promise。**本质上来说就是一个promise是某个函数的返回对象，你可以把回调函数绑定在这个对象上，而不是把回调函数当做参数传入函数。**

```javascript
    //老式函数

    function successCallback(result){
        console.log('it successed with'+result);
    }
    function failureCallback(error){
        console.log('it failed with'+error);
    }
    doSomething(successCallback,failureCallback);

    //新式函数

    let promise = doSomething();
    promise.then(successCallback,failureCallback);
    //或者 : 异步函数调用
    doSomething().then(successCallback,failureCallback)
```
promise 保证点
* 在javascript事件队列的当前运行完成之前，回调函数永远不会被调用
* 通过.then形式添加的回调函数，甚至都在异步操作完成之后才被添加的函数，都会被调用，如上所示
* 通过多次调用.then,可以添加多个回调函数，它们会按照插入顺序并且独立运行

#### 链式调用
> 一个常见的需求是连续两个或多个异步操作，这样的情况下，每一个后来的操作都在前一个执行成功的前提之后，带着上一步返回的结果开始执行。我们可以创造一个promise chain来完成这个需求。

```javascript
//老式代码
doSomething(function(result){
    doSomething(function(newresult){
        doSomething(function(finalresult){
            console.log('Got the final result: ' + finalresult);
        },failureCallback)
    },failureCallback)
},failureCallback)
//现代函数
doSomething()
    .then(function(result){
        return doSomethingElse(result);
    })
    .then(function(newresult){
        return doThirdTing(newresult);
    })
    .then(function(finalresult){
        console.log('Got the final result: ' + finalresult);
    })
    .catch(failureCallback)
```
### promise 实战
> 处理后一个ajax 依赖前一个ajax的结果的请求

```javascript
//先定义一个返回Promise对象的Ajax过程
var ajax = function(option){
    return new Promise(function(resolve, reject){
        $.ajax({
            url: option.url,
            type: option.type || 'get',
            data: option.data || '',
            success: function(data){
                resolve(data);
            },
            error: function(error){
                reject(error);
            }
        });
    });
};

//启动第一个异步任务
var p1 = ajax({
    url: 'url1',
    method:'post',
    data:{
    	code:'xxx'
    }
});
//处理第一个异步回调的结果
p1.then(function(resp1Data){
    console.log(resp1Data);
    <!--  启动第二个异步任务 -->
    return ajax({
        url: 'url2'
    });
})
//处理第2个异步任务的结果
.then(function(resp2Data){
    console.log(resp2Data);
});

```
> 处理多个ajax之间的请求相互不影响，但是最后执行语句的情况是要求所有ajax都已经执行完毕，返回结果的情况

```javascript
/*jquery 的 $.when就是利用promise实现*/

//jquery 封装的when
function getDataFun(){
    var fun1 = $.ajax({url: "/equip_rank",type:'GET',dataType:'jsonp'}),
        fun2 = $.ajax({url: "/score_rank",type:'GET',dataType:'jsonp'}),
        fun3 = $.ajax({url: "/billionaire_rank",type:'GET',dataType:'jsonp'});
    $.when(fun1,fun2,fun3).then(function(data1,data2,data3){
        //成功回调，所有请求正确返回时调用
        console.log(data1[0]);
        console.log(data2);
        console.log(data3);
    },function(){
        //失败回调，任意一个请求失败时返回
        console.log('fail!!');
    })
}

//promise

var ajax = function(options){
	return new Promise(function(resolve,reject){
		$.ajax({
			url:options.url,
			type:options.type || 'get',
			data:options.data || {},
			success(res){
				resolve(res);
			},
			error(res){
				reject(res);
			}
		})
	})
}
var p1 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}}),
	p2 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}}),
	p3 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}});
Promise.all([p1,p2,p3]).then(function(results){
    results.forEach(function(result){
        console.log(result.statusCode);
    });
}).catch(function(err){
    console.log(err);
});

//实例

function testPromise(){
    var ajax = function(option){
        return new Promise(function(resolve,reject){
            $.ajax({
                url:option.url,
                type:option.type || 'get',
                data:option.data || {},
                success(data){
                    resolve(data);
                },
                error(data){
                    reject(data);
                }
            })
        })
    }
    // 获取用户信息
    var p1 = ajax({
        url:'/api/website/user/info/',
        type:'get'
    });
    // 微信签名
    var p2 = ajax({
        url:'/api/website/signature/weixin/',
        type:'post',
        data:{
            url:location.href,
            type:'pay'
        }
    });
    // 获取商品信息
    var p3 = ajax({
        url:'/api/website/pay/product/info/',
        type:'post',
        data:{
            products:'44bd8d05d4f44c629a493b1754da6dc0'
        }
    });

    // 异步请求函数
    Promise.all([p1,p2,p3]).then(function(results){
        results.forEach(function(result){
            console.log('all====>',JSON.stringify(result));
        });
    }).catch(function(err){
        console.log(err);
    });
    // 同步请求函数
    p1.then(function(resp1) {
      console.log('resp1', JSON.stringify(resp1));
      console.log(123);
      return p2;
    }).then(function(resp2) {
      console.log(234);
      console.log('resp2', JSON.stringify(resp2))
      return p3;
    }).then(function(resp3) {
      console.log(345);
      console.log('resp3', JSON.stringify(resp3))
    });


    //测试Promise.all返回的时间的
    console.time('startpromise');
    var s1 = new Promise((resolve,reject) => {
        setTimeout(() => {resolve("s1")},1000)
    });
    var s2 = new Promise((resolve,reject) => {
        setTimeout(() => {resolve("s2")},2000)
    });
    var s3 = new Promise((resolve,reject) => {
        setTimeout(() => {resolve("s3")},3000)
    });
    Promise.all([s1,s2,s3])
        .then(function(results){
            console.log(results);
            console.timeEnd('startpromise');
        })
}
```
![图片](http://oqt0cgoq9.bkt.clouddn.com/example-promise.jpeg)

### promise 模拟实现过程
#### 一个简单版本的实现
```javascript
// 初步构建
function Promise (fn) {
    // 需要一个成功时的回调
    var doneCallback;
    // 一个实例的方法，用来注册异步事件
    this.then = function(done) {
        doneCallback = done;
    }
    function resolve() {
        doneCallback();
    }
    fn(resolve)
}
```
#### 一个添加链式版本的实现
```javascript
// 加入链式支持
function Promise(fn) {
    // 需要成功时的回调
    var doneList = [];
    this.then = function(done, fail){
        doneList.push(done);
        return this;
    }
    function resolve(){
        setTimeout(funciton(){
            doneList.forEach(function(fulfill) {
                fulfill()
            })
        }, 0)
    }
    fn(resolve)
}
// 加入状态机制
function Promise(fn) {
    var state = 'pending';
    var doneList = [];
    this.then = function(done) {
        switch(state) {
            case 'pending':
                doneList.push(done);
                return this;
                break;
            case 'fulfilled':
                done();
                return this;
                break;
        }
    }
    function resolve() {
        state = 'fulfilled';
        setTimeout(function() {
            doneList.forEach(function(fulfill) {
                fulfill();
            })
        }, 0)
    }
    fn(resolve);
}
```
#### 最后一版的实现
```javascript
// 最后一版实现promise
function Promise(fn){
  var state = 'pending';
  var doneList = [];
  var failList= [];
  this.then = function(done ,fail){
    switch(state){
      case "pending":
        doneList.push(done);
        //每次如果没有推入fail方法，我也会推入一个null来占位
        failList.push(fail || null);
        return this;
        break;
      case 'fulfilled':
        done();
        return this;
        break;
      case 'rejected':
        fail();
        return this;
        break;
    }
  }
  function resolve(newValue){
    state = "fulfilled";
    setTimeout(function(){
      var value = newValue;
      for (var i = 0;i<doneList.length;i++){
        var temp = doneList[i](value);
        if(temp instanceof Promise){
            var newP =  temp;
            for(i++;i<doneList.length;i++){
                newP.then(doneList[i],failList[i]);
            }
        }else{
            value = temp;
        }
      }
    },0);
  }
  function reject(newValue){
    state = "rejected";
    setTimeout(function(){
      var value = newValue;
      var tempRe = failList[0](value);
      //如果reject里面传入了一个promise，那么执行完此次的fail之后，将剩余的done和fail传入新的promise中
      if(tempRe instanceof Promise){
        var newP = tempRe;
        for(i=1;i<doneList.length;i++){
            newP.then(doneList[i],failList[i]);
        }
      }else{
        //如果不是promise，执行完当前的fail之后，继续执行doneList
        value =  tempRe;
        doneList.shift();
        failList.shift();
        resolve(value);
      }
    },0);
  }
  fn(resolve,reject);
}
// test
var p = function (){
    return new Promise(function(resolve,reject){
        setTimeout(function(){
          reject('p 的结果');
        }, 100);
    });
}
var p2 = function (input){
    return new Promise(function(resolve){
        setTimeout(function(){
            console.log('p2拿到前面传入的值：' + input)
            resolve('p2的结果');
        }, 100);
    });
}
p()
    .then(
        function(res){
            console.log('p的结果:' + res);
            return 'p then方法第一次返回'
        },
        function(value){
            console.log(value);
            return 'p then方法第一次错误的返回'
        }
    )
    .then(function(res){
        console.log('p第一次then方法的返回：'+res);
        return 'p then方法第二次返回'
    })
    .then(p2)
    .then(function(res){
        console.log('p2的结果：' + res)
    });

```

[好文地址](https://developers.google.com/web/fundamentals/primers/promises#promise-terminology)
