---
title: css-other
date: 2018-04-03 22:41:06
tags: Css
keywords: css，css font-family，css font-weight，font-family和font-weight的关系，bfc
---
### css 杂记
#### font-family 和 font-weight的关系
##### font-weight
> <font color="red">值的取值:</font>「font-weight」的取值范围 normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 | inherit

> <font color="red">normal bold 定义: </font>CSS 2.1 中规定 normal 等价于 400，bold 等价于 700

> <font color="red">font-weight 定义的作用:</font> font-weight,不是告诉浏览器用多**重**的颜色来绘制文字。而是告诉浏览器**在font-family匹配到一个字体集合中如何继续匹配字重要求的字体**

值对应的字体
```
100 - Thin
200 - Extra Light (Ultra Light)
300 - Light
400 - Normal
500 - Medium
600 - Semi Bold (Demi Bold)
700 - Bold
800 - Extra Bold (Ultra Bold)
900 - Black (Heavy)
```
在某字体族真的给出那么多字重的字体时，每个数值对应的字体自重效果都是不同的，400 和 500 的差别就体现出来了。

##### font-family
> CSS属性font-family允许您通过给定一个有先后顺序的，由字体名或者字体族名组成的列表来为选定的元素设置字体。 属性的值用逗号隔开。浏览器会选择列表中第一个该计算机上有安装的字体，或者是通过 @font-face 指定的可以直接下载的字体。

语法说明
* 系统将选择列表中最先可用的字体来显示文字;
* 因为规则1，通常在最末添加一个 generic-family 字体系列名，保证文字获得相似的显示效果;
* 因为规则1，西文字体名应该写在中文字体前，这样才能中英文同时使用不同字体;
* 字体名为中文或包含空格等时，需要加双引号””才能正确识别;
* 中文字体建议也是用其对应英文字体名，如”微软雅黑”为”Microsoft YaHei”，以提高编码兼容性。

##### @font-face 浏览器支持
> [查看文档](http://w3help.org/zh-cn/causes/RF1001)

##### 参考文献
> [w3](https://www.w3.org/TR/css-fonts-3/#font-weight-prop)
  [知乎大神顾轶灵](https://www.zhihu.com/question/20352846)

##### 好文推荐
> [font](http://justineo.github.io/slideshows/font/#/)

#### BFC
##### 定义
> 浮动元素和绝对定位元素，非块级盒子的块级容器（inline-blocks, table-cells, 和 table-captions）以及overflow不为visiable的块级盒子，都会为他们的内容创建新的BFC

##### 创建BFC的方式
* 元素的`float` 不是 `none`
* 元素的`postion`值是`absolute`或`fixed`
* 元素的`display`值是`inline-block` || `table-cell`(HTML表格单元格默认为该值) || `table-caption`(HTML表格标题默认为该值) || `flow-root`
* `overflow`不为`visible`的块元素
* 弹性元素 (`display` 为 `flex` 或 `inline-flex`元素的直接子元素)
* 网格元素 (`display` 为 `grid` 或 `inline-grid` 元素的直接子元素)

**<font color="pink">创建了块格式化上下文的元素中的所有内容都会被包含到该BFC中</font>, <font>BFC中的元素的布局是不受外界的影响</font>**

##### BFC特性
* BFC内部BOX会在垂直方向，从顶部开始一个一个的放置
* BFC内Box垂直方向的距离由margin决定，属于同一个BFC两个相邻的BOXmargin会发生叠加
* BFC区域不会与float BOX叠加
* BFC是页面上一个独立的容器，里面的元素不会受到外面的影响，反之亦然。
* 计算BFC高度的时候，浮动元素也会参与计算。

##### 参考资料
> [深入理解](https://www.w3cplus.com/css/understanding-bfc-and-margin-collapse.html), [MDN](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)