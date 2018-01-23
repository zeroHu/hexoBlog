---
title: css-grid
date: 2018-01-23 18:09:52
tags: Css
---
### css-grid
> grid 是一组相交的水平线和垂直线，特点：固定或弹性的轨道尺寸，定位项目，创建额外的轨道来保存项目，对齐控制，控制折叠内容。

#### 简单创建
```css
display: grid;
或者
display: inline-grid;
```
举例子
```html
<div id="wapper">
    <div>one</div>
    <div>two</div>
    <div>three</div>
    <div>four</div>
    <div>five</div>
</div>
```
```css
#wapper {
    display: grid;
}
```
http://blog.zeroyh.cn/main/css/grid/#wrapper

#### 网格轨道
> 我们通过grid-template-columns 和 grid-template-rows 属性来定义网格中的行和列，这些属性定义了网格的轨道，一个网格轨道就是网格中任意两条线之间的内容

接下来我们添加grid-template-columns属性
```css
#wapper {
+   grid-template-columns: 200px 200px 200px;
}
```
http://blog.zeroyh.cn/main/css/grid/#grid

#### fr单位
> 轨道可以用任何单位进行定义，网格还引入了fr为我们创建灵活的轨道，fr单位表示：网格空间中可用空间的一等份。

```css
#wapper {
+   gird-template-columns: 1fr 1fr 1fr;
或者
+   gird-template-columns: 2fr 1fr 1fr;
或者
+   gird-template-columns: 300px 1fr 1fr;
}
```
http://blog.zeroyh.cn/main/css/grid/#fr

#### 在轨道清单中使用repeat()
简介的说就是 如果 gird-template-columns 分成20 份  如果我们需要些 20个 1fr 1fr 1fr...就显得比较弱鸡了
所以出现了 repeat()
gird-template-columns: repeat(20, 1fr)
所以综合用法就是
gird-tempate-columns: 200px repeat(3, 1fr 3fr) 10px //repeat(3, 1fr 3fr)是1fr 后面跟一个3fr 这样重复3次

#### 隐式和显式网格






