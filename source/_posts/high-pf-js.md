---
title: highPFJavascript
date: 2017-09-12 16:17:49
tags: 高性能JavaScript
---
### 高性能JavaScript总结
#### 减少HTTP请求
* 图片使用 css Sprites(雪碧图)将多个图片集合在一个http请求上面，减少图片的请求
* 使用data:URL展示图片。缺点：
    * 此方案不适合mobile应用。
    * IE7以下不支持
    * 跨页面不会被缓存
* 合并脚本和样式表
* Multipart XHR+
    * 运行客户端用一个HTTP请求就可以从服务端传递多个资源。它通过在服务端将资源（CSS文件，HTML片段，Javascript代码或者base64编码的图片）打包成一个由双方约定的字符串分割的长字符串，并发送到客户端。
然后用Javascript代码处理这个长字符串，并根据他的mime-type类型和传入的其他‘头信息’解析出每个资源。
    ```
        eg:将所有的图片通过定义成一个串来处理
        function splitImages(imageString){
          var imageData = imageString.split('\u0001');
          var imageElement;

          for (var i =0, len = imageData.length; i<len; i++){
            imageElement = document.createElement('img');
            imageElement.src = 'data:image/jpeg;base64,' + imageData[i];
            document.getElementById('container').appendChild(imageElement);
          }
        }
    ```

#### 使用CDN
* 使用cdn 内容发布网络(CDN)是一组分布在多个不同地理位置的WEB服务器，用于更加有效地向用户发布内容。
CDN用于发布静态内容，如图片，脚本，样式表和Flash。

#### 使用缓存
* 条件GET请求
  * 如果浏览器在其缓存中保留了资源的一个副本，但并不确定它是否有效，就会生成一个条件GET请求。如果确认缓存的副本依然有效，浏览器就可以使用缓存中的副本，这会得到更小的响应和更快的用户体检。
  * request: If-Modified-Since: Wed, 22 Feb 2006 04:15:22 GMT
  * response: Last-Modified: Wed, 22 Feb 2006 04:15:22 GMT
  * 缺点：条件GET请求和304响应有助于让页面加载更快，但仍需要客户端和服务器之间进行一次往返确认。
* 添加Expires头
  * Expire头通过确定指明浏览器是否可以使用资源的缓存副本
* 添加Cache-Control
  * http1.1 使用cache-control 来克制expire的缺点。使用cache-control优先级高于expires,可以使用max-age指令指定资源被缓存多久，以秒为单位，如果从资源被请求开始过去的秒数少于max-age，浏览器就使用缓存的版本。

#### css 和 js 放在脚本的位置
* css 放在头部 浏览器必须要等样式表加载完毕之后才渲染页面。
* js 放在尾部
  * 并行下载
    每个主机对于同一域名，可并行请求N个资源文件。
    Chrome的N=6;
    所以，资源文件放在多个主机下，整体响应时间可以加快。但是，多个主机会导致DSN查找时间加大。所以，需要权衡。（3-4）个主机是比较优雅的。
  * 脚本堵塞下载

#### 避免CSS表达式
* css 触发频率太高
#### 使用外部JS和CSS
* 纯粹来讲，内联的JS和CSS可以产生比外部文件文件更快的响应速度。
  但是现实中，外部链接的JS和CSS文件会产生较快的页面，是因为JS和CSS文件有可能被缓存

#### 减少DNS查找
* DNS也是开销。通常浏览器查找一个给定主机名的IP地址要花费20~120毫秒。在DNS查找完成之前，浏览器不能从主机名哪里下载任何东西。+
* DNS缓存
  可以缓存在局域网一台缓存服务器上
  浏览器优先缓存DNS记录（只能缓存一定数量的记录）
  操作系统可以缓存（无数量上限）
  只要cline-server之间保持TCP连接打开状态，就无需DNS查找。
  通过使用Keep-Alive和较少的域名来减少DNS查找

#### 精简JavaScript Css
 * 对js css 进行压缩

#### 避免重定向


