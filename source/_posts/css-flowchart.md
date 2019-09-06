---
title: css-flowchart
date: 2019-09-06 18:11:22
tags: css, css流程图，css flowchart, css flow, 流程图, css 流程图
---

### css flowchar

> In the longtime, I think the flowchart is difficult for me. so when I see the article by chance. so exciting !!! by the way, no one is write by myself. crying...

#### 01

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
    content: '';
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
    content: '';
    height: 100%;
    border-left: 2px solid #eee9dc;
    position: absolute;
    left: -50px;
}
.entry:after {
    content: '';
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

#### doc

> [css flowchart](https://freefrontend.com/css-flowcharts/)
