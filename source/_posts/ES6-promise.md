---
title: ES6-promise
date: 2017-07-10 19:14:47
tags: promise
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
var p1 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}}).resolve(),
	p2 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}}).resolve(),
	p3 = ajax({url:'xxxx',type:'post',data:{xxx:'fff'}}).resolve();

```
