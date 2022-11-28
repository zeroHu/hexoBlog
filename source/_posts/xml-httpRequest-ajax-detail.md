---
title: ajax 请求参数详情，cache 理解
date: 2017-08-18 15:56:38
tags: XMLHttpRequest
keywords: url， http结构， request header参数详解， response header详解，ajax参数解释，缓存机制
---
### url参数详解

#### url的组成部分

```
schema://host[:port#]/path/.../[?query-string][#anchor]
scheme               指定低层使用的协议(例如：http, https, ftp)

host                   HTTP服务器的IP地址或者域名

port#                 HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如 http://www.cnblogs.com:8080/

path                   访问资源的路径

query-string       发送给http服务器的数据

anchor-             锚
```
#### http是无状态协议
#### http 消息结构
```
request 结构：
1）Request line
2）Request header
3）body

response 结构：
1）Response line
2）Response header
3）body

```
#### Request Header 参数详解

```
Cache
    If-Modified-Since: 把浏览器请求时间发给服务器
    Pragma: 防止页面被缓存
        Pargma只有一个用法， 例如： Pragma: no-cache
        注意: 在HTTP/1.0版本中，只实现了Pragema:no-cache
    Cache-Control: 这个是非常重要的规则。 这个用来指定Response-Request遵循的缓存机制。各个指令含义如下
        Cache-Control:Public    可以被任何缓存所缓存（）
        Cache-Control:Private   内容只缓存到私有缓存中
        Cache-Control:no-cache  所有内容都不会被缓存
```
```
Client 头域
    Accept: 浏览器端可以接受的媒体类型
        Accept: */*  代表浏览器可以处理所有类型,(一般浏览器发给服务器都是发这个)
    Accept-Encoding：浏览器申明自己接收的编码方法，通常指定压缩方法，是否支持压缩，支持什么压缩方法（gzip，deflate）
        Accept-Encoding: gzip, deflate
    Accept-Language：浏览器申明自己接收的语言
        Accept-Language: en-us
    User-Agent：告诉HTTP服务器， 客户端使用的操作系统和浏览器的名称和版本
    Accept-Charset：浏览器申明自己接收的字符集，这就是本文前面介绍的各种字符集和字符编码
```
```
Cookie/Login 头域
    Cookie：最重要的header, 将cookie的值发送给HTTP 服务器
    Content-Length：发送给HTTP服务器数据的长度
    Content-Type：发送类型
        Content-Type: application/x-www-form-urlencoded; charset=UTF-8
        Content-Type：application/json;charset=UTF-8

```
```
Miscellaneous 头域
    Referer：提供了Request的上下文信息的服务器，告诉服务器我是从哪个链接过来的，比如从我主页上链接到一个朋友那里，他的服务器就能够从HTTP Referer中统计出每天有多少用户点击我主页上的链接访问他的网站。

```
```
Transport 头域
    Connection：Connection: keep-alive   当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接
    Connection: close  代表一个Request完成后，客户端和服务器之间用于传输HTTP数据的TCP连接会关闭， 当客户端再次发送Request，需要重新建立TCP连接。
    Host:（发送请求时，该报头域是必需的）请求报头域主要用于指定被请求资源的Internet主机和端口号，它通常从HTTP URL中提取出来的
```
#### HTTP Response header

```
Cache头域
    Date: 生成消息的具体时间和日期
    Expires: 浏览器会在指定过期时间内使用本地缓存
    Vary:
        Vary: Accept-Encoding
    Cookie/Login 头域
        P3P:用于跨域设置Cookie, 这样可以解决iframe跨域访问cookie的问题
    Set-Cookie: 非常重要的header, 用于把cookie 发送到客户端浏览器， 每一个写入cookie都会生成一个Set-Cookie.
    Entity头域: ETag作用:  和If-None-Match 配合使用。
    Last-Modified: 用于指示资源的最后修改日期和时间。（实例请看上节的If-Modified-Since的实例）
    Content-Type:WEB服务器告诉浏览器自己响应的对象的类型和字符集
        Content-Type: text/html; charset=utf-8
        Content-Type:text/html;charset=GB2312
        Content-Type: image/jpeg
    Content-Length: 指明实体正文的长度，以字节方式存储的十进制数字来表示。在数据下行的过程中，Content-Length的方式要预先在服务器中缓存所有数据，然后所有数据再一股脑儿地发给客户端。
    Content-Encoding: WEB服务器表明自己使用了什么压缩方法（gzip，deflate）压缩响应中的对象。
```
```
Miscellaneous 头域
    Server:指明HTTP服务器的软件信息
    X-AspNet-Version:如果网站是用ASP.NET开发的，这个header用来表示ASP.NET的版本
    X-Powered-By:表示网站是用什么技术开发的
```
```
Transport头域
    Connection:keep-alive   当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接
```
```
Location头域
    Location: 用于重定向一个新的位置, 包含新的URL地址

```

### ajax参数详解
#### Content-Type 这个是不区分大小写的，可以写为content-type
> 用于定义用户的浏览器或相关设备如何显示将要加载的数据，或者如何处理将要加载的数据
MIME：MIME类型就是设定某种扩展名的文件用一种应用程序来打开的方式类型，当该扩展名文件被访问的时候，浏览器会自动使用指定应用程序来打开。多用于指定一些客户端自定义的文件名，以及一些媒体文件打开方式。

#### 类型
* text/plain(默认) 将文件设置为纯文本的形式，浏览器在获取到这种文件时并不会对其进行处理
* application/x-www-form-urlencoded 窗体数据被编码为名称/值对。这是标准的编码格式
* multipart/form-data 窗体数据被编码为一条消息，页上的每个控件对应消息中的一个部分。
* text/html 浏览器在获取到这种文件时会自动调用html的解析器对文件进行相应的处理。

#### Cache-Control 通用消息头被用于在http 请求和响应中通过指定指令来实现缓存机制。缓存指令是单向的, 这意味着在响应里设置的指令，在请求中不用包含相同的指令。

#### 缓存请求指令

* Cache-Control: max-age=<seconds>
* Cache-Control: max-stale[=<seconds>]
* Cache-Control: min-fresh=<seconds>
* Cache-control: no-cache
* Cache-control: no-store
* Cache-control: no-transform
* Cache-control: only-if-cached

#### 缓存响应指令：

* Cache-control: must-revalidate
* Cache-control: no-cache
* Cache-control: no-store
* Cache-control: no-transform
* Cache-control: public
* Cache-control: private
* Cache-control: proxy-revalidate
* Cache-Control: max-age=<seconds>
* Cache-control: s-maxage=<seconds>

#### 缓存解释：

`public`
表明响应可以被任何对象（包括：发送请求的客户端，代理服务器，等等）缓存。
`private`
表明响应只能被单个用户缓存，不能作为共享缓存（即代理服务器不能缓存它）。
`no-cache`
强制所有缓存了该响应的缓存用户，在使用已存储的缓存数据前，发送带验证器的请求到原始服务器
`only-if-cached`
表明如果缓存存在，只使用缓存，无论原始服务器数据是否有更新。

#### 地址
> [参阅文章](http://www.cnblogs.com/lexus/archive/2012/02/21/2360944.html)
