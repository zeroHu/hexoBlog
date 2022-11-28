---
title: css-layout (css布局)
date: 2017-08-01 10:43:52
tags: Css
keywords: layout, css布局，常见的float布局篇，常见的flex
---

### 布局篇

#### css 常见的 flex 布局篇

![图片](http://static.zeroyh.cn/css-layout-1.jpg)

```css
/*css*/
div.container-flex {
    display: flex;
    width: 300px;
}
.container-flex img {
    vertical-align: middle;
}
.container-flex div {
    flex: 1;
    border: 1px solid red;
}
.container-flex .div2 {
    flex: 2;
}
```

```html
<!-- flex html -->
<div class="container-flex">
    <div class="div1">
        <img src="http://static-image.xfz.cn/1501208125_337.jpg" alt="" />
    </div>
    <div class="div2">
        7月27日早间，红岭创投董事长周世平在“红岭社区”发帖称，网贷不是红岭擅长和看好的，最终会被清理出去，“清盘”过渡期大概要三年，到2020年年底，会将“现有产品全部清理完成”。
        红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收存量，周世平的此番言论迅速让媒体和行业都炸开了锅。
        为什么突然说要清盘？接下来红岭要怎么做？网贷行业会怎么走？记者第一时间采访了周世平，还原周世平最原始、最真实的回答。
    </div>
</div>
```

#### 常见的 float 布局篇

![图片](http://static.zeroyh.cn/css-layout-2.jpg)

```css
/*css*/
.container-float {
    margin-top: 50px;
    width: 300px;
}
.container-float img {
    width: 100px;
    vertical-align: bottom;
}
.right {
    font-size: 20px;
    line-height: 1;
}
.clearfix:after {
    content: '';
    display: block;
    height: 0;
    visibility: hidden;
    clear: both;
}
.container-float .left {
    float: left;
}
```

```html
<!-- float -->
<div class="container-float">
    <div class="left">
        <img
            src="http://static-image.xfz.cn/1501208125_337.jpg"
            alt=""
            width="800"
            height="200"
        />
    </div>
    <div class="right clearfix">
        红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收存量，周世平的此番言论迅速让媒体和行业都炸开了锅。红岭作为网贷行业一，周世平的此番言论迅速让媒体和行业都炸开了锅。红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收
    </div>
</div>
<div style="border:1px solid red">
    <p>i am test clearfix</p>
</div>
```

#### 常见的 inline-block 布局篇

![图片](http://static.zeroyh.cn/css-layout-3.jpg)

```css
/*css*/
.container-inlineBlock div {
    display: inline-block;
    vertical-align: top;
    width: 20px;
    height: 20px;
    background: #ccc;
    margin: 10px;
}
```

```html
<!-- inline-block -->
<div class="container-inlineBlock">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
<div style="border:1px solid red">
    <p>i am test display inline block</p>
</div>
```

#### 定宽不定高的列自动排列布局

##### 数列排列的（colmun-count: n ） 不定高自动排列布局

```html
<ul class="contaner">
    <li class="item">
        <div style="height: 160px;background: pink;">1</div>
    </li>
    <li class="item">
        <div style="height: 285px;background: grey;">2</div>
    </li>
    <li class="item">
        <div style="height: 105px;background: yellow;">3</div>
    </li>
    <li class="item">
        <div style="height: 285px;background: green;">4</div>
    </li>
    <li class="item">
        <div style="height: 185px;background: red;">5</div>
    </li>
</ul>
```

css3 新增的 column 解决方案

```css
.contaner {
    column-count: 3; /*css3新增，把contaner容器中的内容分为三列*/
    column-gap: 20px; /*定义列之间的间隙为20px*/
}
.item {
    font-size: 40px;
    -webkit-column-break-inside: avoid;
    break-inside: avoid;
    counter-increment: item-counter;
}
```

![图片](http://static.zeroyh.cn/layout-col.jpeg)

flex-flow 公用 dom

```html
<div class="container">
    <div class="item" style="height: 40px"></div>
    <div class="item" style="height: 190px"></div>
    <div class="item" style="height: 170px"></div>
    <div class="item" style="height: 120px"></div>
    <div class="item" style="height: 160px"></div>
    <div class="item" style="height: 180px"></div>
    <div class="item" style="height: 140px"></div>
    <div class="item" style="height: 150px"></div>
    <div class="item" style="height: 170px"></div>
    <div class="item" style="height: 170px"></div>
</div>
```

##### 数列排列(flex-flow: column wrap) 不定高自动排列布局 (shu 向排列)

```css
.container {
    display: flex;
    flex-flow: column wrap;
    align-content: space-between;
    /* 容器必须有固定高度且高度大于最高的列高 */
    height: 660px;
    counter-reset: items;
}

.item {
    width: 32%;
    background: #ccc;
    margin-bottom: 20px;
}

/* 仅用于打印数字 */
.item::before {
    counter-increment: items;
    content: counter(items);
}
/* 强制换列 */
.container::before,
.container::after {
    content: '';
    flex-basis: 100%;
    width: 0;
    order: 2;
}
```

![图片](http://static.zeroyh.cn/layout-flex.jpeg)

##### 数列排列(flex-flow: column wrap) 不定高自动排列布局 (横向排列)

```css
.container {
    display: flex;
    flex-flow: column wrap;
    align-content: space-between;
    /* 容器必须有固定高度且高度大于最高的列高 */
    height: 660px;
    /* 非必须 */
    background-color: #f7f7f7;
    border-radius: 3px;
    padding: 20px;
    width: 60%;
    margin: 40px auto;
    counter-reset: items;
}

.item {
    width: 32%;
    /* 非必须 */
    position: relative;
    margin-bottom: 2%;
    border-radius: 3px;
    background-color: #a1cbfa;
    border: 1px solid #4290e2;
    color: #fff;
    padding: 15px;
    box-sizing: border-box;
}

/* 仅用于打印数字 */
.item::before {
    counter-increment: items;
    content: counter(items);
}

/* 将内容块重排为3列 */
.item:nth-child(3n + 1) {
    order: 1;
}
.item:nth-child(3n + 2) {
    order: 2;
}
.item:nth-child(3n) {
    order: 3;
}

/* 强制换列 */
.container::before,
.container::after {
    content: '';
    flex-basis: 100%;
    width: 0;
    order: 2;
}
```

![图片](http://static.zeroyh.cn/layout-flex-2.jpeg)
