---
title: vue-nginx
date: 2017-11-24 11:17:09
tags: nginx
---
#### vue 之nginx配置
> vue的项目如果是配置在域名根目录下(http://xxx.xx.com)，那就是非常简单 没啥好说的直接上nginx代码

```bash
    server {
        listen 80;
        server_name http://xxx.xx.com;
        location / {
                root /xxx/xxxx/vue/dist/;//项目的目录
                try_files $uri $uri/ /index.html =404;//histroy模式需要
        }
    }
```
> vue的项目如果是要配置在域名的某个目录下(http://xxx.xx.com/vue),接下来谈论一下这块

    重要的4个参数，先说一下
    1. config 文件下的index处的 assetsPublicPath   指的是:正式发布环境下编译输出的上线路径的根路径
    2. vuerouter mode   指的是使用的模式
    3. vuerouter base   指的是应用的基路径
    4. nginx 里面的root 换为 alias 具体为啥 下面指出

    如果是hash模式
        1）指定assetsPublicPath 的路径为 /vue （vue 为域名后面的目录名称 即是http://xxx.xx.com/[vue]） 或者是 ./ 这样指的就是当前目录 而并非根目录

    如果是history模式
        hash 1)
        2): vuerouter mode : histroy
        3): vuerouter base : 指定为/vue 也就是域名后面的根目录名称
nginx配置
```bash
    location /vue {
        alias /Users/hujianxia/zeroDemo/vue-demo-longtime/dist/;
        try_files $uri $uri/ /index.html =404;
    }
```
#### nginx root 和 alias 的区别

    root 和 alias 都可以用在location中，都是用来表示指定请求的资源的真是路径，

    但是root 可以使用在 server ，http ，和location 当中，

    而alias 只能使用在location中 并且alias 指定的路径一定要以/结尾 不然会找不到资源,而 root 则对 ”/” 可有可无。

比如
```
    root
        location /i/ {
            root /home/data;
        }
        请求 http://foofish.net/i/top.gif 这个地址时，那么在服务器里面对应的真正的资源是 /home/data/i/top.gif文件，注意真实的路径是root指定的值加上location指定的值。

    alias
        location /i/ {
            alias /home/data/;
        }
        请求 http://foofish.net/i/top.gif 这个地址时，那么在服务器里面对应的真正的资源是 /home/data/top.gif文件

```
> tips:nginx root和alias 参考文章:https://foofish.net/nginx-root-different-with-alias.htmls

