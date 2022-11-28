---
title: css-flowchart
date: 2019-09-06 18:11:22
tags: Css
keywords: css, css流程图，css flowchart, css flow, 流程图, css 流程图
---

### css flowchar

> In the longtime, I think the flowchart is difficult for me. so when I see the article by chance. so exciting !!! by the way, no one is write by myself. crying...

#### 01 Lateral flowchart（侧向流程图）

![effect image](http://static.zeroyh.cn/flowchart-1.png)

```html
<div id="wrapper">
    <span class="label">Root</span>
    <div class="branch lv1">
        <div class="entry">
            <span class="label">Entry-1</span>
            <div class="branch lv2">
                <div class="entry">
                    <span class="label">Entry-1-1</span>
                    <div class="branch lv3">
                        <div class="entry sole">
                            <span class="label">Entry-1-1-1</span>
                        </div>
                    </div>
                </div>
                <div class="entry">
                    <span class="label">Entry-1-2</span>
                    <div class="branch lv3">
                        <div class="entry sole">
                            <span class="label">Entry-1-2-1</span>
                        </div>
                    </div>
                </div>
                <div class="entry">
                    <span class="label">Entry-1-3</span>
                    <div class="branch lv3">
                        <div class="entry sole">
                            <span class="label">Entry-1-3-1</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="entry"><span class="label">Entry-2</span></div>
        <div class="entry">
            <span class="label">Entry-3</span>
            <div class="branch lv2">
                <div class="entry"><span class="label">Entry-3-1</span></div>
                <div class="entry"><span class="label">Entry-3-2</span></div>
                <div class="entry">
                    <span class="label">Entry-3-3</span>
                    <div class="branch lv3">
                        <div class="entry">
                            <span class="label">Entry-3-3-1</span>
                        </div>
                        <div class="entry">
                            <span class="label">Entry-3-3-2</span>
                            <div class="branch lv4">
                                <div class="entry">
                                    <span class="label">Entry-3-3-2-1</span>
                                </div>
                                <div class="entry">
                                    <span class="label">Entry-3-3-2-2</span>
                                </div>
                            </div>
                        </div>
                        <div class="entry">
                            <span class="label">Entry-3-3-3</span>
                        </div>
                    </div>
                </div>
                <div class="entry"><span class="label">Entry-3-4</span></div>
            </div>
        </div>
        <div class="entry"><span class="label">Entry-4</span></div>
        <div class="entry"><span class="label">Entry-5</span></div>
    </div>
</div>
```

```css
*,
*:before,
*:after {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}

body {
    min-width: 1200px;
    margin: 0;
    padding: 50px;
    color: #eee9dc;
    font: 16px Verdana, sans-serif;
    background: #2e6ba7;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

#wrapper {
    position: relative;
}

.branch {
    position: relative;
    margin-left: 250px;
}
.branch:before {
    content: "";
    width: 50px;
    border-top: 2px solid #eee9dc;
    position: absolute;
    left: -100px;
    top: 50%;
    margin-top: 1px;
}

.entry {
    position: relative;
    min-height: 60px;
}
.entry:before {
    content: "";
    height: 100%;
    border-left: 2px solid #eee9dc;
    position: absolute;
    left: -50px;
}
.entry:after {
    content: "";
    width: 50px;
    border-top: 2px solid #eee9dc;
    position: absolute;
    left: -50px;
    top: 50%;
    margin-top: 1px;
}
.entry:first-child:before {
    width: 10px;
    height: 50%;
    top: 50%;
    margin-top: 2px;
    border-radius: 10px 0 0 0;
}
.entry:first-child:after {
    height: 10px;
    border-radius: 10px 0 0 0;
}
.entry:last-child:before {
    width: 10px;
    height: 50%;
    border-radius: 0 0 0 10px;
}
.entry:last-child:after {
    height: 10px;
    border-top: none;
    border-bottom: 2px solid #eee9dc;
    border-radius: 0 0 0 10px;
    margin-top: -9px;
}
.entry.sole:before {
    display: none;
}
.entry.sole:after {
    width: 50px;
    height: 0;
    margin-top: 1px;
    border-radius: 0;
}

.label {
    display: block;
    min-width: 150px;
    padding: 5px 10px;
    line-height: 20px;
    text-align: center;
    border: 2px solid #eee9dc;
    border-radius: 5px;
    position: absolute;
    left: 0;
    top: 50%;
    margin-top: -15px;
}
```

[effect address](http://www.zeroyh.cn/css/cssMagic/cssFlowchart.html)

#### 02 Stand flowchart (竖向流程图)

![effect image](http://static.zeroyh.cn/cssflowchart2.png)

```html
<nav class="nav">
    <ul>
        <li>
            <a href="#">Home</a>
            <ul>
                <li>
                    <a href="#">Lab</a>
                    <ul>
                        <li>
                            <a href="#">Code</a>
                            <ul>
                                <li>
                                    <a href="#">Html</a>
                                    <ul>
                                        <li>
                                            <a href="#">Css</a>
                                            <ul>
                                                <li>
                                                    <a href="#">Jquery</a>
                                                </li>
                                            </ul>
                                        </li>
                                    </ul>
                                </li>
                            </ul>
                        </li>
                        <li>
                            <a href="#">Graph</a>
                            <ul>
                                <li>
                                    <a href="#">Image</a>
                                    <ul>
                                        <li>
                                            <a href="#">Design</a>
                                        </li>
                                    </ul>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li>
                    <a href="#">Blog</a>
                    <ul>
                        <li>
                            <a href="#">Category</a>
                            <ul>
                                <li>
                                    <a href="#">Code</a>
                                </li>
                                <li>
                                    <a href="#">Graph</a>
                                </li>
                            </ul>
                        </li>
                    </ul>
                </li>
                <li>
                    <a href="#">About</a>
                    <ul>
                        <li>
                            <a href="#">Vcard</a>
                        </li>
                        <li>
                            <a href="#">Map</a>
                        </li>
                    </ul>
                </li>
            </ul>
        </li>
    </ul>
</nav>
```

```css
* {
    position: relative;
    margin: 0;
    padding: 0;
    border: 0 none;
}

h1 {
    padding-top: 40px;

    color: #ccc;
    text-align: center;
    font-size: 1.8rem;

    text-shadow: rgba(0, 0, 0, 0.6) 1px 0, rgba(0, 0, 0, 0.6) 1px 0,
        rgba(0, 0, 0, 0.6) 0 1px, rgba(0, 0, 0, 0.6) 0 1px;
}

.nav {
    margin: 20px auto;
    width: 505px;
    min-height: auto;
}

.nav ul {
    position: relative;
    padding-top: 20px;
}

.nav li {
    position: relative;
    padding: 20px 3px 0 3px;
    float: left;

    text-align: center;
    list-style-type: none;
}

.nav li::before,
.nav li::after {
    content: "";
    position: absolute;
    top: 0;
    right: 50%;
    width: 50%;
    height: 20px;
    border-top: 1px solid #ccc;
}

.nav li::after {
    left: 50%;
    right: auto;

    border-left: 1px solid #ccc;
}

.nav li:only-child::after,
.nav li:only-child::before {
    content: "";
    display: none;
}

.nav li:only-child {
    padding-top: 0;
}

.nav li:first-child::before,
.nav li:last-child::after {
    border: 0 none;
}

.nav li:last-child::before {
    border-right: 1px solid #ccc;
    border-radius: 0 5px 0 0;
}

.nav li:first-child::after {
    border-radius: 5px 0 0 0;
}

.nav ul ul::before {
    content: "";
    position: absolute;
    top: 0;
    left: 50%;
    border-left: 1px solid #ccc;
    width: 0;
    height: 20px;
}

.nav li a {
    display: inline-block;
    padding: 5px 10px;

    border-radius: 5px;
    border: 1px solid #ccc;

    text-decoration: none;
    text-transform: uppercase;
    color: #ccc;
    font-family: arial, verdana, tahoma;
    font-size: 11px;
}

.nav li a:hover,
.nav li a:hover + ul li a {
    color: #000;
    background: #c8e4f8;
    border: 1px solid #94a0b4;
}

.nav li a:hover + ul li::after,
.nav li a:hover + ul li::before,
.nav li a:hover + ul::before,
.nav li a:hover + ul ul::before {
    content: "";
    border-color: #94a0b4;
}
```

[effect address](http://www.zeroyh.cn/css/cssMagic/cssFlowchart.html)

#### doc

> [css flowchart](https://freefrontend.com/css-flowcharts/)
