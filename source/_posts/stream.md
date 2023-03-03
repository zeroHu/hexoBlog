---
title: stream
date: 2023-03-03 11:42:10
tags: node
---

### 文件流

1. 可以对大文件进行操作

Stream 有四种流类型:
. Readable - 可读性
. Writable - 可写性
. Duplex - 可读可写性
. Transform - 操作被写入数据，然后读出结果

所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：
. data - 当有数据可读时触发
. end - 没有更多的数据可读时触发
. error - 在接收和写入过程中发生错误时触发
. finish - 所有数据已被写入到底层系统时触发

#### 引入方式

```javascript
const fs = require('fs')
const { createReadStream, createWriteStream } = require('fs')
```

#### 从流中读取数据

```javascript
const readStream = createReadStream('input.txt')
readStream.setEncoding('utf8')
let data = ''
// 处理流事件
readerStream.on('data', function (chunk) {
  data += chunk
})

readerStream.on('end', function () {
  console.log(data) // 这里就是输出了文件内容
})

readerStream.on('error', function (err) {
  console.log(err.stack)
})

console.log('程序执行完毕')
```

#### 写入流文件

```javascript
let data = '我是写入文件的内容'
// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt')

// 使用 utf8 编码写入数据
writerStream.write(data, 'UTF8')

// 标记文件末尾
writerStream.end()

// 处理流事件 --> finish、error
writerStream.on('finish', function () {
  console.log('写入完成。')
})

writerStream.on('error', function (err) {
  console.log(err.stack)
})

console.log('程序执行完毕')
```

#### 管道流

```javascript
// 创建一个可读流
var readerStream = fs.createReadStream('input.txt')

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt')

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream)
```

#### 链式流(压缩+解压)

```javascript
var fs = require('fs')
var zlib = require('zlib')

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'))

// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input.txt'))
```
