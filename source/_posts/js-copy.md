---
title: js-copy
date: 2017-07-31 16:06:38
tags: javascript
---
### js 复制功能
> 原文地址 http://web.jobbole.com/86054/
> 核心代码是document.execCommand('copy')复制代码
```
html
<input type="text" id="twitter" value="hello zero i am" />
<button data-copytarget="#twitter">copy</button>
如果是要复制div内的内容则方法是写一个input框放在页面外 position:absolute left:-3000000px;定义在页面的外部（不可以用hidden 或者display:none）

js
(function() {
  'use strict';
  // click events
  document.body.addEventListener('click', copy, true);
  // event handler
  function copy(e) {
    // find target element
    var
      t = e.target,
      c = t.dataset.copytarget,
      inp = (c ? document.querySelector(c) : null);
    // is element selectable?
    if (inp && inp.select) {
      // select text
      inp.select();
      try {
        if (document.execCommand('copy')) {
          // copy text
          document.execCommand('copy');
          inp.blur();
        } else {
          alert('您的浏览器暂不支持复制功能，请手动复制');
        }
      } catch (err) {
        alert('您的浏览器暂不支持复制功能，请手动复制');
      }
    }
  }
})();
```