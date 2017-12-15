---
title: css-layout (css布局)
date: 2017-08-01 10:43:52
tags: Css
---
### 布局篇

#### css 常见的flex 布局篇
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-layout-1.jpg)
```css
/*css*/
div.container-flex {
  display: flex;
  width:300px;
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
    <img src="http://static-image.xfz.cn/1501208125_337.jpg" alt="">
  </div>
  <div class="div2">7月27日早间，红岭创投董事长周世平在“红岭社区”发帖称，网贷不是红岭擅长和看好的，最终会被清理出去，“清盘”过渡期大概要三年，到2020年年底，会将“现有产品全部清理完成”。 红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收存量，周世平的此番言论迅速让媒体和行业都炸开了锅。 为什么突然说要清盘？接下来红岭要怎么做？网贷行业会怎么走？记者第一时间采访了周世平，还原周世平最原始、最真实的回答。
  </div>
</div>
```

#### 常见的float布局篇
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-layout-2.jpg)
```css
/*css*/
.container-float {
  margin-top: 50px;
  width:300px;
}
.container-float img {
  width:100px;
  vertical-align: bottom;
}
.right {
  font-size: 20px;
  line-height: 1;
}
.clearfix:after {
  content: "";
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
    <img src="http://static-image.xfz.cn/1501208125_337.jpg" alt="" width="800" height="200">
  </div>
  <div class="right clearfix">红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收存量，周世平的此番言论迅速让媒体和行业都炸开了锅。红岭作为网贷行业一，周世平的此番言论迅速让媒体和行业都炸开了锅。红岭作为网贷行业一家曾经的领军公司，至今仍有约192亿元的待收</div>
</div>
<div style="border:1px solid red">
  <p>i am test clearfix</p>
</div>
```

#### 常见的inline-block布局篇
![图片](http://oqt0cgoq9.bkt.clouddn.com/css-layout-3.jpg)
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
