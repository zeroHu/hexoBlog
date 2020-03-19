---
title: npm-tools
date: 2020-03-18 12:31:45
tags: Tools
keywords: npm 全局安装了哪些包， npm global packages
---

### npm 好用的命令行呢

#### 查看 npm 全局安装了哪里工具

`npm list -g --depath 0`

> explain the command line

-   `npm` the node package manager command line tool

-   `list -g` display a tree of every package fount in the user's folders (if without -g option, will show the current package's dependencies )

-   `--depth 0 | --depth=0` avoid including every packpage's dependencies in the tree view
