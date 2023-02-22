---
title: xlsx-create-and-download
date: 2023-02-21 16:13:44
tags: xlsx
---

### xlsx 生成

#### node 端根据数据库返回生成文件流

```javascript
router.get('/test', ctx => {
  const data = [
    ['姓名', '年龄'],
    ['张三', 20],
    ['李四', 30],
  ]
  const res = xlsx.build([{ name: 'sheet1', data: data }])
  ctx.response.body = res
})
```

#### 前端获取文件流并下载文件

```javascript
fetch('http://localhost:9000/test')
  .then(res => res.blob())
  .then(data => {
    const downloadURL = window.URL.createObjectURL(data)
    const a = document.createElement('a')
    a.style.display = 'none'
    a.href = downloadURL
    a.download = 'fileName.xlsx'
    document.body.appendChild(a)
    a.click()
    document.body.removeChild(a)
    window.URL.revokeObjectURL(downloadURL)
  })
```

#### node 端生成 xlsx 文件存储到文件，接口返回

```javascript
// 生成xlsx文件
let buffer = xlsx.build([
  {
    name: 'sheet1',
    data: xlsxData,
  },
])

// 写入生成excel到文件夹
fs.writeFileSync(path.resolve(__dirname, `files/${fileName}`), buffer, {
  flag: 'w',
})

// 接口返回代碼，将文件夹中的xlsx文件返回
const filePath = path.resolve('/files', fileName)
const send = require('koa-send')

ctx.attachment(filePath)
ctx.set('Content-disposition', `attachment;filename="${fileName}"`)
await send(ctx, filePath)
```

#### 前端直接 a 标签获取

```javascript
<a href="xxxxxx" download>下载</a>
```
