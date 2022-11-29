---
title: frp
date: 2022-11-28 21:28:02
tags:
---
frp：

下载地址：https://github.com/fatedier/frp

服务端配置：（frps.ini)

![](frp-01.png)

用户A（客户端1）：（frpc.ini)
![](frp-02.png)
访问地址1：

173.xxx.xx.14:56801 就会转到你本地的 127.0.0.1:7778端口

用户B(客户端2)：（frpc.ini)
![](frp-03.png)

访问地址2：

173.xxx.xx.14:56802 就会转到你本地的 127.0.0.1:7779 端口