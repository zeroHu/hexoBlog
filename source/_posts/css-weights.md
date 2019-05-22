---
title: css-weights
date: 2018-03-21 16:28:54
tags: Css
keywords: css 权重
---
### CSS 权重
> 权重决定了css规则怎样被浏览器解析到生效，即你的css规则是如何被显示的

#### 权重之比
**!important > 内联 > ID > 类 = 伪类 = 属性 > 标签(元素) = 伪元素 > 通配符**

**名词解释**

名词 | 举例解释 | 权重值
--------|----------------
内联 | html文档中的定义的sytle, style="color:red" | 1000
ID | 元素的一种标识，#div | 100
类/伪类/属性 | .class / :hover 或者 :focus / p[class~="important"] | 10
元素/伪元素 | div,p,a / ::after,::before,::first-letter,::first-line,::selecton | 1

#### 权重数量叠加
* `行内样式` + 1000
* ID + 100
* 类 | 伪类 | 属性 +10
* 元素 | 伪元素 +1

#### 权重计算

```css
body #content .data img:hover
```
**body +1, #content +100, .data +10, img +1, :hover +10  最后是0122**

#### 几条规则
* 同样权重的，以最后一个为样式
* 不同权重的，权重高生效
* **慎重用 !important **这样会破坏权重规则

[本文参考链接](https://www.w3cplus.com/css/css-specificity-things-you-should-know.html)

