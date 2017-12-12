---
title: wechat-token
date: 2017-12-02 16:11:53
tags: wechat
---
#### 如何填写微信公众号的基本配置
![wehchat-token](http://oqt0cgoq9.bkt.clouddn.com/wechat-token.jpeg)

##### 设置这个服务器的token

> 这个token虽然文档里面都是说是你自己设置的 ，为了验证。。。。然后天真无邪（傻逼）的我就认为我随便写点啥就行了，然后点击确定的时候就发现要么服务器报错，要么token错误。。。我心想为啥自己随便起的还会错误。。。才知道是需要取你填写的url里面验证的。。。。。。

> 下面的是nodejs 验证token的方式。运行在服务器，配置正确就行，然后点击 在微信公众号输入 url token 。。。 点击。。。终于成功了


nodejs 代码
```
// checkSignature.js
/**
 * 整个验证步骤分为三步
 *    1. 将token、timestamp、nonce三个参数进行字典序排序
 *    2. 将三个参数字符串拼接成一个字符串进行sha1加密
 *    3. 开发者获得加密后的字符串可与signature对比，标识该请求来源于微信
 */


const http = require('http');
const url = require('url');
const crypto = require('crypto');


// Web 服务器端口
const port = 3006;
// 微信公众平台服务器配置中的 Token
const token = 'thisisjszeroyhcntokenonly';


/**
 *  对字符串进行sha1加密
 * @param  {string} str 需要加密的字符串
 * @return {string}     加密后的字符串
 */
function sha1(str) {
  const md5sum = crypto.createHash('sha1');
  md5sum.update(str);
  const ciphertext = md5sum.digest('hex');
  return ciphertext;
}

/**
 * 验证服务器的有效性
 * @param  {object} req http 请求
 * @param  {object} res http 响应
 * @return {object}     验证结果
 */
function checkSignature(req, res) {
  const query = url.parse(req.url, true).query;
  console.log('Request URL: ', req.url);
  const signature = query.signature;
  const timestamp = query.timestamp;
  const nonce = query.nonce;
  const echostr = query.echostr;
  console.log('timestamp: ', timestamp);
  console.log('nonce: ', nonce);
  console.log('signature: ', signature);
  // 将 token/timestamp/nonce 三个参数进行字典序排序
  const tmpArr = [token, timestamp, nonce];
  const tmpStr = sha1(tmpArr.sort().join(''));
  console.log('Sha1 String: ', tmpStr);
  // 验证排序并加密后的字符串与 signature 是否相等
  if (tmpStr === signature) {
    // 原样返回echostr参数内容
    res.end(echostr);
    console.log('Check Success');
  } else {
    res.end('failed');
    console.log('Check Failed');
  }
}


const server = http.createServer(checkSignature)
server.listen(port, () => {
  console.log(`Server is runnig ar port ${port}`);
  console.log('Start Checking...');
});
```
nginx 配置
```
upstream nodejs {
    server 127.0.0.1:3333;
    keepalive 64;
}

server {
    listen 80;
    server_name wechat.nodejh.com;
    # 日志
    access_log /var/log/nginx/wechat.nodejh.com.log;
    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host  $http_host;
        proxy_set_header X-Nginx-Proxy true;
        proxy_set_header Connection "";
        proxy_pass http://nodejs;
    }
}
```

> 原文地址:https://github.com/nodejh/nodejh.github.io/issues/24


