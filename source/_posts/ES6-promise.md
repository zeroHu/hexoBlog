---
title: ES6-promise
date: 2017-07-10 19:14:47
tags: Promise
---
### promise

> 处理后一个ajax 依赖前一个ajax的结果的请求

```
<!-- 先定义一个返回Promise对象的Ajax过程 -->
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
<!--  启动第一个异步任务 -->
var p1 = ajax({
    url: 'url1',
    method:'post',
    data:{
    	code:'xxx'
    }
});
<!-- 处理第一个异步回调的结果 -->
p1.then(function(resp1Data){
    console.log(resp1Data);
    <!--  启动第二个异步任务 -->
    return ajax({
        url: 'url2'
    });
})
<!--处理第2个异步任务的结果 -->
.then(function(resp2Data){
    console.log(resp2Data);
});

```
> 处理多个ajax之间的请求相互不影响，但是最后执行语句的情况是要求所有ajax都已经执行完毕，返回结果的情况

```
jquery 的 $.when就是利用promise实现
<!-- jquery 封装的when -->
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

<!-- promise -->
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




<!-- 实例 -->


testPromise(){
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

    // 同时请求函数
    Promise.all([p1,p2,p3]).then(function(results){
        results.forEach(function(result){
            console.log('all====>',JSON.stringify(result));
        });
    }).catch(function(err){
        console.log(err);
    });
    // 连续函数
    p1.then(function(resp1){
        console.log('resp1',JSON.stringify(resp1));
        console.log(123);
        return p2.then(function(resp2){
            console.log('resp2',JSON.stringify(resp2))
            console.log(234);
            return p3.then(function(resp3){
                console.log('resp3',JSON.stringify(resp3));
                console.log(345);
            })
        })
    });
}
```
![图片](http://oqt0cgoq9.bkt.clouddn.com/example-promise.jpeg)
