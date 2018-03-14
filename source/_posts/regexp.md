---
title: regular expressions
date: 2018-03-14 11:02:20
tags: regexp
---
### 一些经常用但还是记不住的正则表达式
#### 时间校验正则表达式
```javascript
var YYYYMMDDReg = /[\d]{4}[\/-]{1}[\d]{1,2}[\/-]{1}[\d]{1,2}/g;
var YYYYMMDDHHmmReg = /[\d]{4}[\/-]{1}[\d]{1,2}[\/-]{1}[\d]{1,2}\s[\d]{1,2}[:][\d]{1,2}/g;
var YYYYMMDDHHmmssReg = /[\d]{4}[\/-]{1}[\d]{1,2}[\/-]{1}[\d]{1,2}\s[\d]{1,2}[:][\d]{1,2}[:][\d]{1,2}/g;
var HHmmssReg = /[\d]{1,2}[:][\d]{1,2}[:][\d]{1,2}/g;
var HHmmReg = /[\d]{1,2}[:][\d]{1,2}/g;
```
#### 手机的正则表达式
```javascript
var phoneReg = /^1[3|4|5|7|8|][0-9]{9}$/
```
#### 邮箱的正则表达式
```javascript
var emailReg = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/
```
