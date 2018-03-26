---
title: XMLHttpRequest
date: 2017-08-18 11:00:38
tags: XMLHttpRequest
---
### ajax的真面目
#### ajax一直在使用，使用起来相对简单，之前也看过其本质。但是久之就遗忘了。故记录下来
```javascript
  //jquery 的简便使用方法
  $.ajax({
      url: 'http://xxxx.xxx.xxx',//请求的url
      type: 'GET',//请求类型
      data:{//请求参数
          key1:value1
          key2:value2
      },
      success:function(res){//成功回调

      },
      error:function(res){//失败回调

      }
  })
```
#### 何为ajax

> AJAX stands for Asynchronous JavaScript and XML. AJAX is a new technique for creating better, faster, and more interactive web applications with the help of XML, HTML, CSS, and Java Script。翻译过来就是AJAX代表异步JavaScript和XML。 AJAX是在XML，HTML，CSS和Java脚本的帮助下创建更好，更快，更具交互性的Web应用程序的新技术。总结就是我们使用XMLHttpRequest对象来发送一个Ajax请求

#### XMLHttpRequest1
##### 包含:
* xhr.readyState：XMLHttpRequest对象的状态，等于4表示数据已经接收完毕。
* xhr.status：服务器返回的状态码，等于200表示一切正常。
* xhr.responseText：服务器返回的文本数据
* xhr.responseXML：服务器返回的XML格式的数据
* xhr.statusText：服务器返回的状态文本。

##### 缺点:
* 只支持文本数据的传送，无法用来读取和上传二进制文件。
* 传送和接收数据时，没有进度信息，只能提示有没有完成。
* 受到"同域限制"（Same Origin Policy），只能向同一域名的服务器请求数据。

```javascript
var xhr = new XMLHttpRequest();
xhr.open('GET','http://xxx.xxx.xx');
xhr.send();
xhr.onreadystatechange = function(){
    if ( xhr.readyState == 4 && xhr.status == 200 ) {
        //请求成功
        alert( xhr.responseText );
    } else {
        alert( xhr.statusText );
    }
}
```
#### XMLHttpRequest2
##### 增加:
* 可以设置HTTP请求的时限。
* 可以使用FormData对象管理表单数据。
* 可以上传文件。
* 可以请求不同域名下的数据（跨域请求）。
* 可以获取服务器端的二进制数据。
* 可以获得数据传输的进度信息。

```javascript
//1.增加timeout功能
xhr.timeout = 3000;
xhr.ontimeout = function(event){
    alert('请求超时！');
}

//2.模拟表单
var formData = new FormData();
formData.append('username', '张三');
formData.append('id', 123456);
xhr.send(formData);

//3.可以用来处理form表单
var form = document.getElementById('myform');
var formData = new FormData(form);
formData.append('secret', '123456'); // 添加一个表单项
xhr.open('POST', form.action);
xhr.send(formData);

//4.上传文件
var formData = new FormData();
for(var i=0;i<files.length;i++){
    formData.append('files[]', files[i]);
}
xhr.send(formData);

//5.跨域资源共享
//使用"跨域资源共享"的前提，是浏览器必须支持这个功能，而且服务器端必须同意这种"跨域"。如果能够满足上面的条件，则代码的写法与不跨域的请求完全一样。

//6.进度信息
//它分成上传和下载两种情况。下载的progress事件属于XMLHttpRequest对象，上传的progress事件属于XMLHttpRequest.upload对象。
xhr.onprogress = updateProgress;
xhr.upload.onprogress = updateProgress;
function updateProgress(event) {
    if (event.lengthComputable) {
        var percentComplete = event.loaded / event.total;
    }
}
```
#### ajax封装
```javascript
function sendAjax() {
  //构造表单数据
  var formData = new FormData();
  formData.append('username', 'johndoe');
  formData.append('id', 123456);
  //创建xhr对象
  var xhr = new XMLHttpRequest();
  //设置xhr请求的超时时间
  xhr.timeout = 3000;
  //设置响应返回的数据格式
  xhr.responseType = "text";
  //创建一个 post 请求，采用异步
  xhr.open('POST', '/server', true);
  //注册相关事件回调处理函数
  xhr.onload = function(e) {
    if(this.status == 200||this.status == 304){
        alert(this.responseText);
    }
  };
  xhr.ontimeout = function(e) { ... };
  xhr.onerror = function(e) { ... };
  xhr.upload.onprogress = function(e) { ... };
  //发送数据
  xhr.send(formData);
}
```
#### ajax 设置 request header
##### 注意点:
* 方法的第一个参数 header 大小写不敏感，即可以写成content-type，也可以写成Content-Type，甚至写成content-Type;
* Content-Type的默认值与具体发送的数据类型有关，【可以发送什么类型的数据】[content-type详解](http://blog.zeroyh.cn/2018/02/08/ajax-http-body/)一节；
* setRequestHeader必须在open()方法之后，send()方法之前调用，否则会抛错；
* setRequestHeader可以调用多次，最终的值不会采用覆盖override的方式，而是采用追加append的方式。下面是一个示例代码：
```javascript
var xhr = new XMLHttpRequest();
var url = 'http://xxx.xxx.xxx';
xhr.open('POST',url,true);
xhr.setRequestHeader('Content-Type', 'application/xml');
xhr.onreadystatechange = function(){
  ...
}
```

