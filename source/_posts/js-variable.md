---
title: js-variable
date: 2022-04-08 21:38:51
tags: javascript
---

### 前端变量命名的规范
> 变量即是用来存储信息的，那么我们js的变量的命名有两个限制

1. 变量名称必须仅包含字母, 数字, 符号 $ 和 _
2. 首字母不能是数字 
3. 非保留字
`break,case,catch,class,const,continue,debugger,default,delete,do,else,
export,extends,finally,for,function,if,import,in,instanceof,new,return,super,switch,this,
throw,try,typeof,var,void,while,with,yield`等
根据以上两则限制，我们可以举出一下例子。

有效的命名:
```
    let username, UserName, USERNAME, username1, u1, _username, $username, u1$, u1_ ...... 等等
```

无效的命名:
```
    let user@, user%, 23user, 2333, !sus1等
```

#### 通用规范
js 一般采用驼峰式命名，eg: isSure, isLong, infoData 等等类似， 如果是一个单词，就直接采用小写， eg: age, sex, name
#### 全大写
但是你肯定也在js里面见到过全是大写定义的变量，比如:
```javascript
const COLORRED = '#F00',
    MAXNUM = 100
```

全大写，一般是代表这个数是一个常量，也就是说不会被改变的数字。
#### _开头
变量私有但可以暴露给外部访问，则用单个下划线。
eg：var _status = false

变量私有且只在特定范围内有效，强烈不建议直接访问，则用双下划线。 
__selfStatus = true

单下划线的私有变量，可以直接访问，但不能用于修改。
双下划线的变量既不能直接访问更不能直接修改。

#### $开头
与关键字或保留字或内置变量同名的变量用前缀符号$表示，并且$应该在下划线后。
eg： $options, $class, __$dirname

#### 函数参数
构造函数应该首字母大写
必填参数小驼峰，选填参数用_xX
```javascript
eg： function Person() {}
var person1 = new Person()

function clone(obj, _isDeep)
```

#### 一般常用场景分析

##### 表示可见性，进行中状态的推荐方式isXxx
```
eg: 
isShow: 是否展示
isVisible: 是否可见
isRunning: 正在运行中
isLoading: 正在加载中
```
##### 配置类，选项类
allowXx表示功能属性，noXx, 不建议
```javascript
allowScale, noDeal
```

##### 函数命名
主动监听采用onXx, 被动处理使用handleXx
```
eg: onSubmit, handleStatusChange, onKeydown 等
```
