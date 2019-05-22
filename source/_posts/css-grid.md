---
title: css-grid
date: 2018-01-23 18:09:52
tags: Css
keywords: css grid，grid，栅栏式布局，网格轨道
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
http://www.zeroyh.cn/main/css/grid/#wrapper

#### 网格轨道
> 我们通过grid-template-columns 和 grid-template-rows 属性来定义网格中的行和列，这些属性定义了网格的轨道，一个网格轨道就是网格中任意两条线之间的内容

接下来我们添加grid-template-columns属性
```css
#wapper {
+   grid-template-columns: 200px 200px 200px;
}
```
http://www.zeroyh.cn/main/css/grid/#grid

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
http://www.zeroyh.cn/main/css/grid/#fr

#### 在轨道清单中使用repeat()
简介的说就是 如果 gird-template-columns 分成20 份  如果我们需要些 20个 1fr 1fr 1fr...就显得比较弱鸡了
所以出现了 repeat()
gird-template-columns: repeat(20, 1fr)
所以综合用法就是
gird-tempate-columns: 200px repeat(3, 1fr 3fr) 10px //repeat(3, 1fr 3fr)是1fr 后面跟一个3fr 这样重复3次

http://www.zeroyh.cn/main/css/grid/#autorows

#### 隐式和显式网格
> 上面的这种 我们使用grid-template-columns 定义了自己的列轨道，让网格按照所需排列。

grid-auto-rows: 100px
```css
#wapper {
+   grid-template-columns: 200px repeat(1, 1fr 3fr) 50px;
+   grid-auto-rows: 100px;
}
```
http://www.zeroyh.cn/main/css/grid/#automix
#### 轨道大小和 minmax()
> 想给网格设定一个最小尺寸，不会低于最小

grid-auto-rows: minmax(100px, auto)
#### 跨轨道放置网格项目
> grid-column-start, grid-column-end, grid-row-start 和 grid-row-end 属性，把前两个元素放到了我们的三列网格中。从左至右，第一个元素从列线1开始，延伸至列线4，也就是我们这个例子中最右边的列线。并从行线1延伸到行线3，占据了两个行轨道。

```css
.rowcolumn {
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: 100px
}
.box1 {
    grid-column-start: 1;
    grid-column-end: 3;
    grid-row-start: 1;
    grid-row-end: 5;
}
.box2 {
    grid-column-start: 2;
    grid-column-end: 6;
    grid-row-start: 1;
    grid-row-end: 4;
}
```
http://www.zeroyh.cn/main/css/grid/#rowcolumn

#### 网格间距
> 网格横向间距  或 网格纵向间距  可使用 grid-column-gap 和 grid-row-gap 属性来创建

```css
    .gap {
        grid-template-columns: repeat(3, 1fr);
        grid-column-gap: 10px;
        grid-row-gap: 1em;
    }
```
http://www.zeroyh.cn/main/css/grid/#gap

#### 允许嵌套网格




