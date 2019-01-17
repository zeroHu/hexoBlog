---
title: css-box-shadow
date: 2017-08-02 09:37:33
tags: Css
---
### box-shadow
> box-shadow 阴影是我们经常用的一个属性，但是却经常想不起来单边的阴影写法，记录下来，方便查阅（本方法 是查阅css secret 所获）

#### 参数解释
box-shadow: h-shadow v-shadow blur spread color inset;

>   **h-shadow (必)： 水平移动距离 正值向右， 负值向左
    v-shadow (必)： 垂直移动距离 正值向下， 负值向上
    blur (选)：     模糊距离
    spread (选)：   阴影尺寸 正直扩大， 负值减少
    color (选)：    阴影颜色
    inset (选):     将外部阴影改为内部阴影**

#### 投影原理解释
![图片](http://static.zeroyh.cn/box-shadow.jpeg)

步骤:
* (1) 以该元素相同的尺寸11和位置，画一个 rgba(0,0,0,.5) 的矩形。
* (2) 把它向右移 2px，向下移 3px。
* (3) 使用高斯模糊算法(或类似算法)将它进行 4px 的模糊处理。这在 本质上表示在阴影边缘发生阴影色和纯透明色之间的颜色过渡长度近似于模 糊半径的两倍(比如在这里是 8px)。
* (4) 接下来，模糊后的矩形与原始元素的交集部分会被切除掉，因此它 看起来像是在该元素的“后面”。这跟大多数开发者所理解的情况(元素叠在模糊后矩形的上层)可能稍有不同。不过，在某些场景下，意识到没有任何投影绘制在元素的下层十分重要。举例来说，如果给元素设置一层半透 明的背景，我们就看不到它下层有任何投影。这一点跟 text-shadow 不同， 因为文字下层的投影不会被裁切。

```css
.box-shadow {
  box-shadow: 2px 3px 4px rgba(0,0,0,.5);
}
```
#### 单边阴影
![图片](http://upload.zeroyh.cn/boxshadow-four.jpeg)
> 原理解析：最终的解决方案来自 box-shadow 鲜为人知的第四个长度参数。它排在 模糊半径参数之后，称作扩张半径。这个参数会根据你指定的值去扩大或 (当指定负值时)缩小投影的尺寸。举例来说，一个 -5px 的扩张半径会把投影的宽度和高度各减少 10px(即每边各 5px)。

```css
/*要素是 阴影值（6px) 和 扩张半径值(-6px) 是相反数*/
div {
    display: inline-block;
    width: 100px;
    height: 100px;
    background: yellow;
    margin-right: 20px;
    vertical-align: top;
    color: red;
}
.box-shadow1 {
    box-shadow: 0 -6px 12px -6px rgba(0, 0, 0, .5);
}
.box-shadow2 {
    box-shadow: 0 6px 12px -6px rgba(0, 0, 0, .5);
}
.box-shadow3 {
    box-shadow: -6px 0 12px -6px rgba(0, 0, 0, .5);
}
.box-shadow4 {
    box-shadow: 6px 0 12px -6px rgba(0, 0, 0, .5);
}

```
#### 邻边阴影
![图片](http://upload.zeroyh.cn/boxshadow-two.jpeg)
> 原理解析:可以使用3个参数的方案，注意调节阴影值和偏移值得大小即可

```css
.box-shadow1 {
    box-shadow: 6px -6px 12px -6px rgba(0, 0, 0, .5);
}
.box-shadow2 {
    box-shadow: -6px 6px 12px -6px rgba(0, 0, 0, .5);
}
```

#### 双侧阴影
![图片](http://upload.zeroyh.cn/boxshadow-three.jpeg)
> 原理解析:当我们想把投影设置在元素的两条对边(比如左侧和右侧)时，事情就 变得棘手了。因为扩张半径在四个方向上的作用是均等的(也就是说，我们 无法指定投影在水平方向上放大，而在垂直方向上缩小)11，唯一的办法是用 两块投影(每边各一块)来达到目的。然后基本上就是把“单侧投影”中的 技巧运用两次:

```css
.box-shadow1 {
    box-shadow: 6px 0 6px -6px #000, -6px 0 6px -6px #000
}
.box-shadow2 {
    box-shadow: 0 6px 6px -6px #000, 0 -6px 6px -6px #000
}
```

#### 三侧阴影
![图片](http://upload.zeroyh.cn/boxshadow-eight.jpeg)
```css
.box-shadow1 {
    box-shadow: 0px 7px 5px -2px blue, 7px 0px 5px -2px red, -7px 0px 5px -2px green;
}
.box-shadow2 {
    box-shadow: 0 -6px 6px -6px rgba(0, 0, 0, .5), -6px 0 6px -6px rgba(0, 0, 0, .5), 0 6px 6px -6px rgba(0, 0, 0, .5)
}
.box-shadow3 {
    box-shadow: -6px 0  6px -6px rgba(0, 0, 0, .5), 6px 0 6px -6px rgba(0, 0, 0, .5), 0 6px 6px -6px rgba(0, 0, 0, .5)
}
.box-shadow4 {
    box-shadow: 0 -6px 6px -6px rgba(0, 0, 0, .5), 6px 0 6px -6px rgba(0, 0, 0, .5), -6px 0 6px -6px rgba(0, 0, 0, .5)
}
.all {
  box-shadow: 0 12px 6px 6px #ccc;
}

```

#### 四侧阴影
![图片](http://upload.zeroyh.cn/boxshadow-six.jpeg)
```css
    .all {
      box-shadow: 0 0 12px #000;
    }
```
