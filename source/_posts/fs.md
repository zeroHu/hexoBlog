---
title: fs
date: 2023-03-03 10:35:25
tags: node
---

### fs 模块

nodejs 的内置模块，主要用于文件操作。下面介绍几种常见用法。
1. 权限介绍
![](fs-01.jpeg)
#### 普通用法

##### 引用方法

```javascript
import * as fs from 'node:fs'
const fs = require('fs')
```

##### 读文件

```javascript
// 异步
fs.readFile(filePath, 'utf8', (err, data) => {
  if (err) throw err
  console.log('data', data)
})
// 同步
const fileResult = fs.readFileSync(filePath, 'utf8')
console.log('data', fileResult)
```

##### 写文件

```javascript

/**
 * options是可选参数, 配置项为
 * {
 *   encoding: {String || null} default = 'utf8',
 *   mode: {Number} default = 438,
 *   flag: {String} default = 'w', flag值，默认为w,会清空文件，然后再写。flag值，r代表读取文件，w代表写文件，a代表追加。
 * }
 */

// 异步
fs.writeFile(fileName, data, [, options], callback)

// 同步
fs.writeFileSync(fileName, data [, options])

```

##### 写文件(追加内容)

```javascript
// 异步
fs.appendFile(fileName, data, [, options], callback)
// 同步
fs.appendFileSync(fileName, data, [, options])
```

##### 拷贝文件

```javascript
// 异步
fs.copyFile(fileNameA, fileNameB, callback)
// 同步
fs.copyFileSync(fileNameA, fileNameB)
```

##### 删除文件

```javascript
// 异步
fs.unlink(filePath, callback)
// 同步
fs.unlinkSync(filePath, callback)
```

##### 文件打开

```javascript
// 大文件操作与上面的有所不同，可以用 fs.open打开，fs.read / fs.write 读写， 最后fs.close 关闭
fs.open(path, flags, [,mode], callback)
fs.close()

// 示例用法
// copy 方法 一般不用这个，可以借助stream
function copy(src, dest, size = 16 * 1024, callback) {
  // 打开源文件
  fs.open(src, 'r', (err, readFd) => {
    // 打开目标文件
    fs.open(dest, 'w', (err, writeFd) => {
      let buf = Buffer.alloc(size);
      let readed = 0; // 下次读取文件的位置
      let writed = 0; // 下次写入文件的位置

      (function next() {
        // 读取
        fs.read(readFd, buf, 0, size, readed, (err, bytesRead) => {
          readed += bytesRead;

          // 如果都不到内容关闭文件
          if (!bytesRead) fs.close(readFd, err => console.log('关闭源文件'));

          // 写入
          fs.write(writeFd, buf, 0, bytesRead, writed, (err, bytesWritten) => {
            // 如果没有内容了同步缓存，并关闭文件后执行回调
            if (!bytesWritten) {
              // fs.fsync 是请求将打开文件描述符的所有数据刷新到存储设备。 具体实现是操作系统和设备特定的。
              fs.fsync(writeFd, err => {
                fs.close(writeFd, err => return !err && callback());
              });
            }
            writed += bytesWritten;

            // 继续读取、写入
            next();
          });
        });
      })();
    });
  });
}
```

#### Promise 用法

##### 引入方法

```javascript
import * as fs from 'node:fs/promises'
const fs = require('fs/promises')
```

##### 使用示例 readFile

```javascript
import { readFile } from 'node:fs/promises'

try {
  const data = await readFile('/tmp/hello')
  console.log('data', data)
} catch (err) {
  console.error('error', err.message)
}
```

所有其他语法promise语法类似......