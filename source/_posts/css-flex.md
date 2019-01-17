---
title: css-flex
date: 2017-09-07 18:10:53
tags: Css
---
### CSS flex 初探
#### flex 一行多个单元格布局
![图片](http://static.zeroyh.cn/css-flex-1.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
<div class="flex-container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```
#### flex布局之垂直居中
![图片](http://static.zeroyh.cn/css-flex-2.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
<div class="flex-middle-center">
    <div>1</div>
</div>
```

#### flex布局之 数列排序
![图片](http://static.zeroyh.cn/css-flex-3.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
<div class="flex-column">
    <div>1</div>
    <div>2</div>
</div>
```

#### flex justify-content示例
![图片](http://static.zeroyh.cn/css-flex-4.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
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

![图片](http://static.zeroyh.cn/css-flex-5.jpg)

#### flex align-items示例
![图片](http://static.zeroyh.cn/css-flex-7.jpg)

```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
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

![图片](http://static.zeroyh.cn/css-flex-6.jpg)

#### flex-wrap示例
![图片](http://static.zeroyh.cn/css-flex-8.jpg)

```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
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
![图片](http://static.zeroyh.cn/css-flex-9.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
<div class="flex-align-content">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```

#### flex margin-right设值
![图片](http://static.zeroyh.cn/css-flex-10.jpg)
```css
/*css内容*/
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
```
```html
<!-- html 内容 -->
<div class="flex-margin-auto">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```
### CSS flex再探 [solved-by-flexbox](https://hufan-akari.github.io/solved-by-flexbox/)
#### 简洁的栅格系统
**栅格系统特性**
* 每一行的每一个栅格默认都是同宽通告，默认自适应
* 为了足够灵活，能够添加尺寸属性到单独的栅格中。没有添加的，仍然简单的平分剩下的可用空间
* 支持响应式布局，可以添加媒体查询到栅格中
* 每一个栅格可以在垂直方向上置顶，置底，居中
* 栅格可以随意嵌套

<font color="red">**basecss**<font>
```css
.grid {
    display: flex;
}

.grid-cell {
    flex: 1;
    background: #ccc;
}
/* 修饰样式属性 不必要*/
.retouch {
    padding: 10px 0;
    margin: 0 10px;
}
```
##### 1/2栅格
![1/2栅格](http://upload.zeroyh.cn/flex-1-2.jpg)
![1/2栅格特性](http://upload.zeroyh.cn/flex-1-2-more.jpg)
```html
<div class="grid">
    <div class="grid-cell retouch">1/2</div>
    <div class="grid-cell retouch">1/2</div>
</div>
```
```css
/*css: basecss*/
```
##### 1/3栅格
![1/3栅格](http://upload.zeroyh.cn/flex-1-3.jpg)
```html
<div class="grid">
    <div class="grid-cell retouch">1/3</div>
    <div class="grid-cell retouch">1/3</div>
    <div class="grid-cell retouch">1/3</div>
</div>
```
```css
/*css: basecss*/
```
##### 百分比尺寸和auto
![1/2auto](http://upload.zeroyh.cn/flex-1-2-auto.jpg)
![1/4auto](http://upload.zeroyh.cn/flex-1-4-auto.jpeg)
```html
<div class="grid">
    <div class="grid-cell retouch grid-1of2">1/2</div>
    <div class="grid-cell retouch">auto</div>
    <div class="grid-cell retouch">auto</div>
</div>
```
```html
<div class="grid">
    <div class="grid-cell retouch">auto</div>
    <div class="grid-cell retouch">auto</div>
    <div class="grid-cell retouch grid-1of4">1/4</div>
    <div class="grid-cell retouch">auto</div>
</div>
```
```css
/* css: basecss */
.grid-1of2 {
    flex: 0 0 50%;
}
.grid-1of4 {
    flex: 0 0 25%;
}
```
##### 对齐属性
![align-items 对齐属性](http://upload.zeroyh.cn/flex-align-items.jpg)
```html
<div class="grid">
    <div class="grid-cell retouch grid-self-top">我是置顶</div>
    <div class="grid-cell retouch">我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的我是内容特别多的</div>
    <div class="grid-cell retouch grid-1of4">我是没加任何属性的</div>
    <div class="grid-cell retouch grid-self-center">我是居中的</div>
    <div class="grid-cell retouch grid-self-bottom">我是置底的</div>
</div>
```
```css
.grid {
    display: flex;
    align-items: flex-start;
}

.grid-cell {
    flex: 1;
    background: #ccc;
}
.grid-self-top {
    align-self: flex-start;
}
.grid-self-center {
    align-self: center;
}
.grid-self-bottom {
    align-self: flex-end;
}
/* css: basecss 中的 retouch ; */
```
#### 圣杯布局
![圣杯式](http://upload.zeroyh.cn/flex-shengbei.jpg)
```html
<div class="holygrid">
    <header>i am header</header>
    <div class="content">
        <main>i am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodi am content bodyi am i am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodi am content bodyi am i am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodi am content bodyi am i am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodyi am content bodi am content bodyi am </main>
        <nav>
            i am nav
        </nav>
        <aside>
            i am aside
        </aside>
    </div>
    <footer>i am footer</footer>
</div>
```
```css
.holygrid {
    display: flex;
    min-height: 100%;
    flex-direction: column;
}
header, footer {
    flex: none;
}
header {
    width: 100%;
    background: #eee;
    height: 50px;
}
footer {
    width: 100%;
    background: #ccc;
    height: 60px;
}
.content {
    display: flex;
}
.content main {
    flex: 1;
}
.content nav {
    order: -1;
}
.content nav, .content aside {
    flex: 0 0 12em;
    padding: 1em;
    background: #999;
}
```
#### 输入input组件
![input button 组件](http://upload.zeroyh.cn/flex-input-grid.jpg)
```html
<div class="input-grid">
    <input type="text">
    <span class="input-button">send</span>
</div>
```
```css
.input-grid {
    display: flex;
}
.input-grid input {
    flex: 1;
    padding: 10px 0;
}
.input-grid span {
    text-align: center;
    border: 1px solid #ccc;
    padding: 10px 0;
    width: 50px;
    border-radius: 0;
    border-left: 0;
}
```
#### 媒体对象
![flex 用于媒体排列](http://upload.zeroyh.cn/flex-media.jpg)
```html
<div class="media">
    <div class="media-figure"></div>
    <div class="media-body">
        <h3>i am title</h3>
        <p>i am des</p>
        <p>i am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am contenti am content</p>
    </div>
</div>
```

```css
.media {
    display: flex;
    align-items: flex-start;
}
.media-figure {
    margin-right: 10px;
    width: 100px;
    height: 100px;
    background: #eee;
}
.media-body {
    flex: 1
}
```



