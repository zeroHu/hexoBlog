---
title: frp-tools
date: 2019-03-05 16:19:58
tags: Tools
---
#### 内网穿透工具之FRP
> 不能免俗的必要谈谈内网穿透的必要性，跟微信打交道就知道了，一言不合就需要跟他交互啊！如果你只是在本地开发，也没个域名。也没个公网ip啥的，人家根本不认识你，咋整。咋写下去！这个时候就需要内网穿透了。把本地的代码用一个公网域名能访问。这样和微信才能正常沟通啊。不会鸡同鸭讲~ 废话少说。 直接开始吧！

![服务器图](http://static.zeroyh.cn/WechatIMG628.png)

[frp文档](https://github.com/fatedier/frp/blob/master/README_zh.md)
[frp下载地址](https://github.com/fatedier/frp/releases)

##### 具体步骤 我就不在frp地址 复制出来了啊。

##### 说几个注意点吧
  1. 我的linux 云服务器是阿里云服务器，我估计腾讯云服务器或者别的应该都有这个问题，我们的端口号需要到安全组去配置
  2. 如果云服务器是nginx配置的话 我这里贴一下nginx配置
  3. 进程守护的话最简单的推荐nohup command & 这种方式。别的也折腾不是



##### 贴一下所有的配置
```nginx
# linux 云服务器的 nginx配置 frp.zeroyh.cn nginx config
map $http_x_forwarded_for $clientRealip {
   "" $remote_addr;
   ~^(?P<firstAddr>[0-9\.]+),?.*$  $firstAddr;
}

server {
       listen 80;
       server_name frp.*;
       location / {
           proxy_pass http://127.0.0.1:8009;  # frps.ini 里的 vhost_http_port = 8009
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $clientRealip;  # $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
}
```

```
# linux 云服务器的 frps 配置
[common]
bind_port = 7000
vhost_http_port = 8009

[web]
type = http
auth_token = xxxx
custom_domains = frp.zeroyh.cn
```


```
#mac 公司内网服务器配置
[common]
server_addr = 47.104.201.127 (这里是你的服务器的公网ip地址)
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[web]
type = http
local_port = 9001
custom_domains = frp.zeroyh.cn
auth_token = xxx
```







