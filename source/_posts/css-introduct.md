---
title: css-introduct
date: 2019-10-21 09:12:32
tags: Css
keywords: css, css-trick, css magic
---

### CSS 漫谈

#### css 是什么？

> 层叠样式表（Cascading Style Sheets)
> 它定义如何显示 HTML 元素。
> 甚至是成为前后端同学最大的分水岭。不得不说还是非常的不起眼而重要呀

#### css 发展史

-   1.1994 年哈肯.维姆莱提出了 css 的最初建议。伯特波斯当时正在设计一个叫做“Argo”的浏览器，他们决定一起合作设计 CSS
-   2.W3C 开始接管 CSS
    1997 年初。W3C 内组织了专门管 CSS 的工作组，其负责人是克里斯李雷
-   3.css2.1
    1988 年 5 月 W3C 发表了 CSS2
    CSS2.1 修改了 CSS2 中的一些错误，删除了其中不被支持的内容和增加了一些已有的浏览器的扩展内容
-   4.CSS3
    从 2011 年开始 CSS 被分为多个模块单独升级。统称为 CSS3

#### css 预处理

> LESS、 SASS(SCSS)、 STYLUS

为什么都拥抱预处理器?

> 语法不够强大，比如无法嵌套书写导致模块化开发中需要书写很多重复的选择器；
> 没有变量和合理的样式复用机制，使得逻辑上相关的属性值必须以字面量的形式重复输出，导致难以维护。

> 主要就讲讲 sass(scss)，其余大致功能相同
> sass 是缩进式写法， scss 是花括号写法。 scss 是后面才支持的。 不过两者之间是可以用命令改变的

```
sass-convert style.sass style.scss
sass-convert style.scss style.sass
```

sass 主要从 variables, nested rules, mixins, functions 稍稍引入

<h3>码界杠精名言：talk is cheap, show me the code !!!</h3>

##### variables

> 变量管理使修改代码主题或者整体样式的时候容易，且避免重复代码，增加可维护性

```scss
/* _variable.scss */
$black: #000 !default;
$themeColor: blue;
```

```scss
/** 基础玩法 **/
@import '_variable';

@use './_variable' with (
  $black: #222
);

body {
    color: $themeColor;
}

.black-div {
    color: $black;
}

.square {
    $size: 100px;
    width: $size;
    height: $size;
    border-radius: $size / 2;
}

/** 高级玩法 **/

$dark-theme: true !default;
$primary-color: #f8bbd0 !default;
$accent-color: #6a1b9a !default;

@if $dark-theme {
    $primary-color: darken($primary-color, 60%);
    $accent-color: lighten($accent-color, 60%);
}

.button {
    background-color: $primary-color;
    border: 1px solid $accent-color;
    border-radius: 3px;
}
```

##### nested rules

> 嵌套使代码可读性强，更加容易编写 css

```scss
/* 基础玩法  */
.div {
    a {
        &:hover {
            text-decoration: underline;
        }
    }

    &-span {
        border: 1px solid red;
    }

    font {
        family: fantasy;
        size: 30em;
        weight: bold;
    }
}
```

##### mixins

> 定义避免重复使用的代码

```scss
/** 基础玩法 **/
@mixin reset-list {
    margin: 0;
    padding: 0;
    list-style: none;
}

@mixin horizontal-list {
    @include reset-list;

    li {
        display: inline-block;
        margin: {
            left: -2px;
            right: 2em;
        }
    }
}

nav ul {
    @include horizontal-list;
}

/** 高级玩法 **/
@mixin rtl($property, $ltr-value, $rtl-value) {
    #{$property}: $ltr-value;

    [dir='rtl'] & {
        #{$property}: $rtl-value;
    }
}

.sidebar {
    @include rtl(float, left, right);
}

@mixin replace-text($image, $x: 50%, $y: 50%) {
    text-indent: -99999em;
    overflow: hidden;
    text-align: left;

    background: {
        image: $image;
        repeat: no-repeat;
        position: $x $y;
    }
}

.mail-icon {
    @include replace-text(url('/images/mail.svg'), 0);
}

@mixin square($size, $radius: 0) {
    width: $size;
    height: $size;

    @if $radius != 0 {
        border-radius: $radius;
    }
}

.avatar {
    @include square(100px, $radius: 4px);
}
```

##### functions

> 处理比较复杂的函数
> 支持的语法， @if, @else, @while, @for, @each ...

```scss
@function pow($base, $exponent) {
    $result: 1;
    @for $_ from 1 through $exponent {
        $result: $result * $base;
    }
    @return $result;
}

.sidebar {
    float: left;
    margin-left: pow(4, 3) * 1px;
}

@function sum($numbers...) {
    $sum: 0;
    @each $number in $numbers {
        $sum: $sum + $number;
    }
    @return $sum;
}

.micro {
    width: sum(50px, 30px, 100px);
}
```

#### css 大神作品

[https://diana-adrianne.com/purecss-francine/](https://diana-adrianne.com/purecss-francine/)
[http://suohb.com/work/flower2.htm](http://suohb.com/work/flower2.htm)
[https://diana-adrianne.com/purecss-pink/](https://diana-adrianne.com/purecss-pink/)
[https://a.singlediv.com/](https://a.singlediv.com/)
[https://www.html5tricks.com/demo/css3-sector-menu/index.html](https://www.html5tricks.com/demo/css3-sector-menu/index.html)

#### thank
