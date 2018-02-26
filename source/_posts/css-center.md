---
title: css3 center(css 居中)
date: 2017-07-18 18:30:10
tags: Css
---
### CSS居中
#### 水平居中初探
##### 块级元素
> 定宽定高div 水平居中

```html
<div class="center">111</div>
```
```css
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

```html
<div class="center">222</div>
```

```css

.center {
  width:200px;
  background:red;
  margin;0 auto;
}
```

##### 行内元素
```html
<span>hello i am a span</span>
```
```css
span {
  text-align:center;
}
```
#### 垂直居中初探
> 宽高是固定的垂直居中

```html
<main>
<h1>Am I centered yet?</h1> <p>Center me, please!</p>
</main>
```

```css
/*绝对定位解决方案*/

main {
  position: absolute;
  top: 50%;
  left: 50%;
  margin-top: -3em; /* 6/2 = 3 */
  margin-left: -9em; /* 18/2 = 9 */
  width: 18em;
  height: 6em;
}

/*简写版*/
main {
  position:absolute;
  top:50%;
  left:50%;
  transform:translate(-50%,-50%);
}


/*非绝对定位解决方案*/

/*(只能用于视口居中的位置)*/
main {
  width: 18em;
  margin: 50vh auto 0;
  transform: translateY(-50%);
}
```
(flex 通用版 部分浏览器支持不太好)
```html
<div class="container">
  <div class="center">xxx</div>
</div>
```
```css
.container {
  margin: auto;
  width: 300px;
  height: 300px;
  background: yellow;
  display: flex;
}
.center {
  background: #ccc;
  padding: 20px;
  margin: auto;
}

```