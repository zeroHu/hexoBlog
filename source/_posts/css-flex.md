---
title: css-flex
date: 2017-09-07 18:10:53
tags: Css
---
### CSS flex 初探
#### flex 一行多个单元格布局
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-1.jpg)
```
.flex-container {
    width: 30px;
    height: 30px;
    display: flex;
    background:#eee;
}

.flex-container div {
    height:30px;
    flex:1;
    border: 1px solid #333;
}

<div class="flex-container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```
#### flex布局之垂直居中
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-2.jpg)
```
.flex-middle-center {
    width: 100px;
    height:100px;
    display: flex;
    align-items: center;
    justify-content: center;
    background:#eee;
}
.flex-middle-center div {
    width: 50px;
    border:1px solid #333;
    text-align: center;
}
<div class="flex-middle-center">
    <div>1</div>
</div>
```

#### flex布局之 数列排序
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-3.jpg)
```
.flex-column {
    display: flex;
    flex-direction: column;
    width: 100px;
    height:100px;
    background:#eee;
}

.flex-column div{
    width: 30px;
    border:1px solid #333;
}
<div class="flex-column">
    <div>1</div>
    <div>2</div>
</div>
```

#### flex justify-content示例
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-4.jpg)
```
.flex-justify-content {
    display: flex;
    width: 100px;
    height:100px;
    background:#eee;
    justify-content: center;
}
.flex-justify-content div {
    width: 30px;
    border:1px solid #333;
}
<div class="flex-justify-content">
    <div>1</div>
    <div>2</div>
</div>
```

> justify-content 的值有
  * flex-start (default)
  * flex-end
  * center
  * space-between
  * space-around

![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-5.jpg)

#### flex align-items示例
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-7.jpg)

```
.flex-align-items {
    display: flex;
    width: 100px;
    height:100px;
    background:#eee;
    align-items:center;
}
.flex-align-items div {
    width: 30px;
    height:30px;
    border:1px solid #333;
}
.flex-align-items div:nth-child(2) {
   height:50px;
}
<div class="flex-justify-content">
    <div>1</div>
    <div>2</div>
</div>
```

> align-items 的值有
  * flex-start (default)
  * flex-end
  * center
  * baseline
  * stretch

![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-6.jpg)

#### flex-wrap示例
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-8.jpg)

```
.flex-wrap {
    display: flex;
    flex-wrap: wrap;
    width: 100px;
    height:100px;
    background:#eee;
}
.flex-wrap div {
    height:30px;
}
.flex-wrap div:nth-child(1){
    width: 20px;
    border:1px solid #333;
}
.flex-wrap div:nth-child(2){
    width: 40px;
    border:1px solid #333;
}
.flex-wrap div:nth-child(3){
    width: 50px;
    border:1px solid #333;
}
.flex-wrap div:nth-child(4){
    width: 60px;
    border:1px solid #333;
}
<div class="flex-wrap">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
</div>
```
> flex-wrap 有的值有
  * nowrap (default)
  * wrap
  * wrap-reverse

#### flex align-content示例
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-9.jpg)
```
.flex-align-content {
    display: flex;
    flex-wrap: wrap;
    align-content:center;
    width: 100px;
    height:100px;
    background:#eee;
}
.flex-align-content div:nth-child(1){
    width: 20px;
    border:1px solid #333;
}
.flex-align-content div:nth-child(2){
    width: 40px;
    border:1px solid #333;
}
.flex-align-content div:nth-child(3){
    width: 50px;
    border:1px solid #333;
}
<div class="flex-align-content">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```

#### flex margin-right设值
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-flex-10.jpg)
```
.flex-margin-auto {
    display: flex;
    width: 100px;
    height:100px;
    background:#eee;
}
.flex-margin-auto div {
    width: 20px;
    border:1px solid #333;
}
.flex-margin-auto div:nth-child(1){
    margin-right:auto;
}

<div class="flex-margin-auto">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```

