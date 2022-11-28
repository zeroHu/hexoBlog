---
title: css-icons
date: 2019-09-11 10:21:45
tags: Css
keywords: css 图标
---

### cssIcon

> [效果查看地址](http://www.zeroyh.cn/css/shape/icons.html) > ![图片预览效果](http://static.zeroyh.cn/icons-1.jpg)

#### flip

```html
<div class="lds-circle">
    <div></div>
</div>
```

```css
.lds-circle {
    display: inline-block;
    transform: translateZ(1px);
}
.lds-circle > div {
    display: inline-block;
    width: 51px;
    height: 51px;
    margin: 6px;
    border-radius: 50%;
    background: #fff;
    animation: lds-circle 2.4s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
@keyframes lds-circle {
    0%,
    100% {
        animation-timing-function: cubic-bezier(0.5, 0, 1, 0.5);
    }
    0% {
        transform: rotateY(0deg);
    }
    50% {
        transform: rotateY(1800deg);
        animation-timing-function: cubic-bezier(0, 0.5, 0.5, 1);
    }
    100% {
        transform: rotateY(3600deg);
    }
}
```

#### route

```html
<div class="lds-dual-ring"></div>
```

```css
.lds-dual-ring {
    display: inline-block;
    width: 64px;
    height: 64px;
}
.lds-dual-ring:after {
    content: " ";
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid #fff;
    border-color: #fff transparent #fff transparent;
    animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
```

#### shake

```html
<div class="lds-facebook">
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
.lds-facebook {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-facebook div {
    display: inline-block;
    position: absolute;
    left: 6px;
    width: 13px;
    background: #fff;
    animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook div:nth-child(1) {
    left: 6px;
    animation-delay: -0.24s;
}
.lds-facebook div:nth-child(2) {
    left: 26px;
    animation-delay: -0.12s;
}
.lds-facebook div:nth-child(3) {
    left: 45px;
    animation-delay: 0;
}
@keyframes lds-facebook {
    0% {
        top: 6px;
        height: 51px;
    }
    50%,
    100% {
        top: 19px;
        height: 26px;
    }
}
```

#### heart

```html
<div class="lds-heart"><div></div></div>
```

```css
.lds-heart {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
    transform: rotate(45deg);
    transform-origin: 32px 32px;
}
.lds-heart div {
    top: 23px;
    left: 19px;
    position: absolute;
    width: 26px;
    height: 26px;
    background: #fff;
    animation: lds-heart 1.2s infinite cubic-bezier(0.215, 0.61, 0.355, 1);
}
.lds-heart div:after,
.lds-heart div:before {
    content: " ";
    position: absolute;
    display: block;
    width: 26px;
    height: 26px;
    background: #fff;
}
.lds-heart div:before {
    left: -17px;
    border-radius: 50% 0 0 50%;
}
.lds-heart div:after {
    top: -17px;
    border-radius: 50% 50% 0 0;
}
@keyframes lds-heart {
    0% {
        transform: scale(0.95);
    }
    5% {
        transform: scale(1.1);
    }
    39% {
        transform: scale(0.85);
    }
    45% {
        transform: scale(1);
    }
    60% {
        transform: scale(0.95);
    }
    100% {
        transform: scale(0.9);
    }
}
```

#### route circle

```html
<!-- ring one -->
<div class="lds-ring">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
<!-- ring two -->
<div class="lds-roller">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
/* ring one */
.lds-ring {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-ring div {
    box-sizing: border-box;
    display: block;
    position: absolute;
    width: 51px;
    height: 51px;
    margin: 6px;
    border: 6px solid #fff;
    border-radius: 50%;
    animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
    animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
    animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
    animation-delay: -0.15s;
}
@keyframes lds-ring {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
/* ring two */
.lds-roller {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-roller div {
    animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    transform-origin: 32px 32px;
}
.lds-roller div:after {
    content: " ";
    display: block;
    position: absolute;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: #fff;
    margin: -3px 0 0 -3px;
}
.lds-roller div:nth-child(1) {
    animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
    top: 50px;
    left: 50px;
}
.lds-roller div:nth-child(2) {
    animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
    top: 54px;
    left: 45px;
}
.lds-roller div:nth-child(3) {
    animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
    top: 57px;
    left: 39px;
}
.lds-roller div:nth-child(4) {
    animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
    top: 58px;
    left: 32px;
}
.lds-roller div:nth-child(5) {
    animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
    top: 57px;
    left: 25px;
}
.lds-roller div:nth-child(6) {
    animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
    top: 54px;
    left: 19px;
}
.lds-roller div:nth-child(7) {
    animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
    top: 50px;
    left: 14px;
}
.lds-roller div:nth-child(8) {
    animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
    top: 45px;
    left: 10px;
}
@keyframes lds-roller {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
```

#### circle size

```html
<div class="lds-default">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
.lds-default {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-default div {
    position: absolute;
    width: 5px;
    height: 5px;
    background: #fff;
    border-radius: 50%;
    animation: lds-default 1.2s linear infinite;
}
.lds-default div:nth-child(1) {
    animation-delay: 0s;
    top: 29px;
    left: 53px;
}
.lds-default div:nth-child(2) {
    animation-delay: -0.1s;
    top: 18px;
    left: 50px;
}
.lds-default div:nth-child(3) {
    animation-delay: -0.2s;
    top: 9px;
    left: 41px;
}
.lds-default div:nth-child(4) {
    animation-delay: -0.3s;
    top: 6px;
    left: 29px;
}
.lds-default div:nth-child(5) {
    animation-delay: -0.4s;
    top: 9px;
    left: 18px;
}
.lds-default div:nth-child(6) {
    animation-delay: -0.5s;
    top: 18px;
    left: 9px;
}
.lds-default div:nth-child(7) {
    animation-delay: -0.6s;
    top: 29px;
    left: 6px;
}
.lds-default div:nth-child(8) {
    animation-delay: -0.7s;
    top: 41px;
    left: 9px;
}
.lds-default div:nth-child(9) {
    animation-delay: -0.8s;
    top: 50px;
    left: 18px;
}
.lds-default div:nth-child(10) {
    animation-delay: -0.9s;
    top: 53px;
    left: 29px;
}
.lds-default div:nth-child(11) {
    animation-delay: -1s;
    top: 50px;
    left: 41px;
}
.lds-default div:nth-child(12) {
    animation-delay: -1.1s;
    top: 41px;
    left: 50px;
}
@keyframes lds-default {
    0%,
    20%,
    80%,
    100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.5);
    }
}
```

#### line circle

```html
<div class="lds-ellipsis">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
.lds-ellipsis {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-ellipsis div {
    position: absolute;
    top: 27px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: #fff;
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
    left: 6px;
    animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
    left: 6px;
    animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
    left: 26px;
    animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
    left: 45px;
    animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
    0% {
        transform: scale(0);
    }
    100% {
        transform: scale(1);
    }
}
@keyframes lds-ellipsis3 {
    0% {
        transform: scale(1);
    }
    100% {
        transform: scale(0);
    }
}
@keyframes lds-ellipsis2 {
    0% {
        transform: translate(0, 0);
    }
    100% {
        transform: translate(19px, 0);
    }
}
```

#### winnower

```html
<div class="lds-hourglass"></div>
```

```css
.lds-hourglass {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-hourglass:after {
    content: " ";
    display: block;
    border-radius: 50%;
    width: 0;
    height: 0;
    margin: 6px;
    box-sizing: border-box;
    border: 26px solid #fff;
    border-color: #fff transparent #fff transparent;
    animation: lds-hourglass 1.2s infinite;
}
@keyframes lds-hourglass {
    0% {
        transform: rotate(0);
        animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
    }
    50% {
        transform: rotate(900deg);
        animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
    }
    100% {
        transform: rotate(1800deg);
    }
}
```

#### halo

```html
<div class="lds-ripple">
    <div></div>
    <div></div>
</div>
```

```css
.lds-ripple {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-ripple div {
    position: absolute;
    border: 4px solid #fff;
    opacity: 1;
    border-radius: 50%;
    animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
    animation-delay: -0.5s;
}
@keyframes lds-ripple {
    0% {
        top: 28px;
        left: 28px;
        width: 0;
        height: 0;
        opacity: 1;
    }
    100% {
        top: -1px;
        left: -1px;
        width: 58px;
        height: 58px;
        opacity: 0;
    }
}
```

#### most use loading

```html
<div class="lds-spinner">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</div>
```

```css
.lds-spinner {
    color: official;
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
}
.lds-spinner div {
    transform-origin: 32px 32px;
    animation: lds-spinner 1.2s linear infinite;
}
.lds-spinner div:after {
    content: " ";
    display: block;
    position: absolute;
    top: 3px;
    left: 29px;
    width: 5px;
    height: 14px;
    border-radius: 20%;
    background: #fff;
}
.lds-spinner div:nth-child(1) {
    transform: rotate(0deg);
    animation-delay: -1.1s;
}
.lds-spinner div:nth-child(2) {
    transform: rotate(30deg);
    animation-delay: -1s;
}
.lds-spinner div:nth-child(3) {
    transform: rotate(60deg);
    animation-delay: -0.9s;
}
.lds-spinner div:nth-child(4) {
    transform: rotate(90deg);
    animation-delay: -0.8s;
}
.lds-spinner div:nth-child(5) {
    transform: rotate(120deg);
    animation-delay: -0.7s;
}
.lds-spinner div:nth-child(6) {
    transform: rotate(150deg);
    animation-delay: -0.6s;
}
.lds-spinner div:nth-child(7) {
    transform: rotate(180deg);
    animation-delay: -0.5s;
}
.lds-spinner div:nth-child(8) {
    transform: rotate(210deg);
    animation-delay: -0.4s;
}
.lds-spinner div:nth-child(9) {
    transform: rotate(240deg);
    animation-delay: -0.3s;
}
.lds-spinner div:nth-child(10) {
    transform: rotate(270deg);
    animation-delay: -0.2s;
}
.lds-spinner div:nth-child(11) {
    transform: rotate(300deg);
    animation-delay: -0.1s;
}
.lds-spinner div:nth-child(12) {
    transform: rotate(330deg);
    animation-delay: 0s;
}
@keyframes lds-spinner {
    0% {
        opacity: 1;
    }
    100% {
        opacity: 0;
    }
}
```
