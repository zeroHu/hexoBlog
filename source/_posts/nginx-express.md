---
title: nginx-express
date: 2017-09-28 17:11:10
tags: nginx
keywords: express 项目的nginx配置，nginx-express配置
---
#### nginx 如何能够代理到express这样的localhost:3000这样的页面
```nginx
upstream express-ip {
    # Nodejs app upstream
    server 127.0.0.1:3000;
    keepalive 64;
}
# Server on port 80
server {
    listen 80;
    server_name hakase-node.co;
    root /home/yume/express-ip;
    location / {
        # Proxy_pass configuration
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_max_temp_file_size 0;
        proxy_pass http://express-ip/;
        proxy_redirect off;
        proxy_read_timeout 240s;
    }
}
```
