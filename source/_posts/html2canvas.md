---
title: html2canvas
date: 2018-03-27 11:25:19
tags: canvas
---
### html2canvas
> 小记： 神器 html2canvas记，是有这么个需求，需要生成一个新闻卡片，然后如果直接用canvas画的情况呢，比较复杂，文本内容需要分段而且还需要控制字数，直接用html，css来写呢就会非常的便捷了，众里寻他千百度。蓦然回首，那人却在，[html2canvas](http://html2canvas.hertzen.com/getting-started/)。使用版本记录：html2canvas 1.0.0-alpha.10

#### 关键代码
```javascript
var canvas = document.querySelector("canvas");
// 这段就是将你要绘制额的html ID 绘制成 canvas
html2canvas(document.querySelector("#share-box-img"), { canvas: canvas }).then(function(canvas) {
    var base64Image = canvas.toDataURL('image/png');
    document.body.appendChild(canvas);
});
// 这个是绘制整个页面 x,y 是坐标 可以用jq 的position().x positon().y获取， width height 是canvas的宽高
html2canvas(document.body, { x: x, y: y, width: width, height: height }).then(function(canvas) {
    document.body.appendChild(canvas);
});
```
#### 注意事项
* 目前还不支持部分css3 属性，我自己测试中不兼容的属性有 box-shadow, css 超出行用...表示
* 如果绘制的img中图片的地址是 非本域名的 需要添加 `useCORS: true`才能绘制出来
* scale 是可以设置缩放比例的

#### 参数配置
> [参数配置地址](http://html2canvas.hertzen.com/configuration)

name | default | description
-----|---------|-------------
async | true | 是否异步解析和渲染元素
allowTaint | false | 是否允许跨域的图像渲染到canvas上
backgroundColor  | #ffffff | canvas的背景色，如果是`none`就是dom上的，如果设置为`null`就是`transparent`透明
canvas | null | 如果传入canvas就用已经存在的在那基础上再绘制
foreignObjectRendering | false | 如果浏览器支持，是否使用ForeignObject呈现
imageTimeout | 15000 | 设置image的超时时间，设置`0`禁止超时
ignoreElements | (element) => false | Predicate function which removes the matching elements from the render（翻译无能）
logging | true | 启用日志记录以进行调试
onclone | null | Callback function which is called when the Document has been cloned for rendering, can be used to modify the contents that will be rendered without affecting the original source document（翻译无能）
proxy | null | `proxy`被用来加载跨域的图像，如果设置为空，跨域的图像将不被加载
removeContainer | true | 是否清除html2canvas暂时创建的dom结构
scale | window.devicePixelRatio | 渲染的时候的缩放倍数，默认是`window.devicePixelRatio`
useCORS| false | 是否尝试从服务器跨域加载图片
width | element width | canvas 宽
height | element height | canvas 高
x | element x-offset | x坐标
y | element y-offset | y坐标
scrollX | element scrollX | 用于element使用了`position:fixed`
scrollY | element scrollY | 用于element使用了`position:fixed`
windowWidth | Window.innerWidth | 用于使用 media query 改变大小的时候
windowHeight | Window.innerHeight | 用于使用media query 改变大小的时候