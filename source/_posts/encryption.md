---
title: encryption
date: 2023-02-21 17:16:00
tags: encryption
---
### 加密方式
介绍加密方式。

#### AES
```javascript
const CryptoJS = require('crypto-js')

const key = CryptoJS.enc.Utf8.parse('xxxxxxxxxxx') //十六位十六进制数作为密钥
const iv = CryptoJS.enc.Utf8.parse('xxxxxxxxxxxxx') //十六位十六进制数作为密钥偏移量

function Encrypt(word) {
  let srcs = CryptoJS.enc.Utf8.parse(word)
  let encrypted = CryptoJS.AES.encrypt(srcs, key, {
    iv: iv,
    mode: CryptoJS.mode.CBC,
    padding: CryptoJS.pad.Pkcs7,
  })
  return encrypted.ciphertext.toString().toUpperCase()
}

function Decrypt(word) {
  let encryptedHexStr = CryptoJS.enc.Hex.parse(word)
  let srcs = CryptoJS.enc.Base64.stringify(encryptedHexStr)
  let decrypt = CryptoJS.AES.decrypt(srcs, key, {
    iv: iv,
    mode: CryptoJS.mode.CBC,
    padding: CryptoJS.pad.Pkcs7,
  })
  let decryptedStr = decrypt.toString(CryptoJS.enc.Utf8)
  return decryptedStr.toString()
}
```

#### RSA

```javascript
const NodeRSA = require('node-rsa')
const publicKey = 'xxxxxxxxxxxxxx'
const privateKey = 'xxxxxxxxxxxxxxxxx'
// 加密
function encrypted(str) {
  const publicKeyObj = new NodeRSA(publicKey)
  publicKeyObj.setOptions({ encryptionScheme: 'pkcs1' })

  const encrypted = publicKeyObj.encrypt(str, 'base64', 'utf8')
  return encrypted
}

// 解密
function decrypted(str) {
  const privateKeyObj = new NodeRSA(privateKey)
  privateKeyObj.setOptions({ encryptionScheme: 'pkcs1' })
  
  const decrypted = privateKeyObj.decrypt(str, 'utf8')
  return JSON.parse(decrypted)
}
```
