---
title: css-other
date: 2018-04-03 22:41:06
tags: Css
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
> [查看文档]http://w3help.org/zh-cn/causes/RF1001

##### 参考文献
> [w3](https://www.w3.org/TR/css-fonts-3/#font-weight-prop)
  [知乎大神顾轶灵](https://www.zhihu.com/question/20352846)

##### 好文推荐
> [font](http://justineo.github.io/slideshows/font/#/)
