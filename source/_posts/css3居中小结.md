---
title: css3居中小结
date: 2017-07-18 18:30:10
tags: CSS
---
### CSS居中
> 定宽定高div 水平居中

```
html
<div class="center">111</div>
css
.center {
  width:200px;
  height:200px;
  background:red;
  margin;0 auto;
}
.center {
  position:absolute;
  left:50%;
  margin-left:100px;
}
```
> 定宽不定高div 水平居中

```
html
<div class="center">222</div>
css
.center {
  width:200px;
  background:red;
  margin;0 auto;
}
```