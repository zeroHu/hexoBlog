---
title: websocket-http2-https
date: 2018-03-09 14:16:56
tags: http
---
### 了解websocket http2 和 http1 和 https的作用是啥
#### websocket
> 简单而又不失礼貌的答复是：websocket最大的特点是 服务器可以向客户端发送消息。

其余特点:
 1) 也是建立在TCP协议之上的，服务器端比较容易实现。
 2) 与http协议有良好的兼容性，默认端口是80和443，并且握手段采用http协议，因此握手时不容易屏蔽，能通过各种http代理服务器。
 3）数据格式比较轻量，性能开销小，通信高效
 4）可以发送文本，也可以发送二进制数据
 5）没有同源限制，客户端可以与任意服务器通话
 6) 协议标识符是 （ws), 如果加密是（wss).服务器网址就是 URL
`wx://example.com:80/some/path`
##### 客户端示例代码
```
let ws = new WebSocket({"wss://echo.websocket.org"})
ws.onopen = evt => {
    console.log('======> connection open <=======');
    ws.send('hello i am from clinet')
}
ws.onmessage = evt => {
    console.log('======> receive data is', evt.data);
    ws.close()
}
ws.onclose = (evt) => {
    console.log('connection closed')
}
```

##### websocket api 讲解
```
let ws = new WebSocket({"wss://echo.websocket.org"})
ws.readyState 返回值
    0: CONNETCTING 正在连接
    1: OPEN 连接成功
    2: CLOSING 正在关闭
    3: CLOSED 关闭成功

ws.onopen 用于指定连接成功后的回调函数
ws.onclose 用于指定连接关闭后的回调函数
ws.onmessage 用于指定收到服务器数据后的回调函数
ws.send()  用于向服务器发送数据

```
##### websocket 服务器端代码实现
>给个代码实现链接吧： [示例代码](https://github.com/joewalnes/websocketd/tree/master/examples)    [阮老师文章链接](http://www.ruanyifeng.com/blog/2017/05/websocket.html)

#### http 协议
> [好文推荐](https://github.com/CyC2018/Interview-Notebook/blob/master/notes/HTTP.md)

##### HTTP是如何建立连接的

![http协议](https://sfault-image.b0.upaiyun.com/335/472/3354729685-59f18143c8c3f_articlex)

##### 发送一条HTTP请求会发生什么
```
获取主机名，例如：http://www.example.com
通过DNS获取服务器IP
获取端口，默认是80端口
连接到 112.23.59.223:80服务器 （这里其实是TCP连接）
通过TCP信道发送一个HTTP请求
服务器读取一个HTTP请求
服务器查找所需资源并通过TCP信道返回资源
关闭TCP连接
```

#### http2
我理解就这下面这几句，具体可以参考 [阮老师的文章](http://www.ruanyifeng.com/blog/2016/08/http.html)
> 1.头信息压缩
  2.支持服务器推送 [阮老师写的](http://www.ruanyifeng.com/blog/2018/03/http2_server_push.html)
  3.对同时连接数量不限制

#### https
感觉太弱了，字都认识，在一起有点懵，[阮老师链接](http://www.ruanyifeng.com/blog/2014/02/ssl_tls.html)
我的自我总结就下面一句话[尴尬]
> 我的理解是在http协议上新增 SSL/TLS 协议，加密保证内容的安全


