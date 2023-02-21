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
