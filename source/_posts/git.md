---
title: git 疑难杂症
date: 2018-05-09 16:49:12
tags: gitTools
---
### git 记录
#### git 中重命名忽略大小写问题
总结起来网上的2大势力
```
1. git config core.ignorecase false // git 设置 记录文件大小写
2. git mv -f OldFileNameCase newfilenamecase // 强制换名
```
> 方法1 不兼容windows，windows下不区分大小写，但是linux是区分大小写的。。。。坑妈呀
  方法2 会产生一个多的文件

可行的方案
```
$ git mv ./name1 ./name1.bak
$ git add .
$ git commit -m "改名（第 1/2 步）"

$ git mv ./name1.bak/ ./name2
$ git commit -m "改名（第 2/2 步）"

$ git push
```

1.[参考文档](https://walterlv.github.io/post/case-insensitive-in-git-rename.html#%E5%B0%9D%E8%AF%95%E5%87%BA%E7%9A%84%E5%8F%AF%E8%A1%8C%E7%9A%84%E6%96%B9%E6%B3%95)
2.[stackoverflow](https://stackoverflow.com/questions/17683458/how-do-i-commit-case-sensitive-only-filename-changes-in-git)

