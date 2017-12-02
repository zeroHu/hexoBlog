---
title: https
date: 2017-12-02 15:59:39
tags: https ssl
---
#### 最新鲜的nginx 配置https 踩坑出来了
> 看到阿里云已经开始不卖免费的ssl证书了，吓得我赶紧取七牛上买了20个放着，想着之前也没给自己的网站配置，感觉需要自己实践一遍，才能出真知啊

废话少说，直接撸代码.下面的代码是直接从服务器上拷贝下来的 ，肯定正常的运行https
```
server {
    listen 80;#如果你想支持http 如果不想就去掉
    listen 443 ssl;

    ssl_certificate /etc/nginx/ssl/jszeroyhcn.crt;
    ssl_certificate_key /etc/nginx/ssl/jszeroyhcn.key;
    keepalive_timeout   70;
    server_name js.zeroyh.cn;
    #禁止在header中出现服务器版本，防止黑客利用版本漏洞攻击
    server_tokens off;
    #如果是全站 HTTPS 并且不考虑 HTTP 的话，可以加入 HSTS 告诉你的浏览器本网站全站加密，并且强制用 HTTPS 访问
    #add_header Strict-Transport-Security "max-age=31536000; includeSubdomains";
    # ......
    fastcgi_param   HTTPS               on;
    fastcgi_param   HTTP_SCHEME         https;
}
```
> 根据我调研了有2中 阿里云上申请的是 .pem 和 .key 七牛云上的上.crt 和 .key 配置方法都一样

  接下来讲述一下为啥说是踩坑，这样很简单的代码我就配置完了，但是接下来的却是让我怎么也理解不了，因为http能够正常的访问，但是https确迟迟没有反应，也不报错，一开始我以为是自己配置出了问题呢，再我查了很多nginx配置后。我开始确信自己的nginx配置是正确的。。。。根据 netstat –apn 命令看到了我的 :443端口是 listen的情况，并且根据网上的排错步骤，我在服务器上wget https://xxx.xxx.xx(域名)/ 就没法连接上。但是 我在服务器上 wget https://127.0.0.1/(这个的前提上这个服务器上的别的nginx都关闭了的情况下 就连接通了)。文件也下载下来了，于是我就确认了问题肯定不是出在我的配置上了。
  
  在找问题的过程中，听到了有的人说是不是安全配置，于是我就去搜了一下阿里云的安全配置（因为我用的是阿里云的服务器）。文档很清晰 ，一下子就找到了，我发现是安全配置里面没有加上443端口，坑爹啊！！！于是我加上这条规则后就能访问https了。特此记录下来以备后面查询和愚笑自己。
