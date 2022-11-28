---
title: js-message-carousel
date: 2019-01-18 18:03:33
tags: javascript
---
### 消息轮播
> 以前没咋想过这个功能，思维被局限于图片轮播的形式了。今儿突发了一种觉得挺棒棒的。记录下来~

#### html
```html
<div class="notice">
  <ul>
    <li>第1条公告第1条公告第1条公告第1条公告第1条公告第1条公告</li>
    <li>第2条公告第2条公告第2条公告第2条公告第2条公告第2条公告</li>
    <li>第3条公告第3条公告第3条公告第3条公告第3条公告第3条公告</li>
    <li>第4条公告第4条公告第4条公告第4条公告第4条公告第4条公告</li>
  </ul>
</div>
```

#### css
```css
  div,ul,li {
    margin: 0;
    padding: 0;
  }

  .notice {
    width: 300px;
    height: 35px;
    padding: 0 30px;
    background-color: #b3effe;
    overflow: hidden;
  }

  .notice ul li {
    list-style: none;
    line-height: 35px;
    display: block;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }
```

#### js
```javascript
  <script src="../jquery.js"></script>
  $(function () {
    // 调用 公告滚动函数
    setInterval(function () {
      var obj = $('.notice ul'); // obj : 动画的节点，本例中是ul
      var top = '-35px'; // top : 动画的高度，本例中是-35px; 注意向上滚动是负数
      var time = 500; // time : 动画的速度，即完成动画所用时间，本例中是500毫秒，即marginTop从0到-35px耗时500毫秒
      $(obj).animate({
        marginTop: top
      }, time, function () { // function : 回调函数，每次动画完成，marginTop归零，并把此时第一条信息添加到列表最后
        $(this).css({
          marginTop: "0"
        }).find(":first").appendTo(this);
      })
    }, 2000);
  });
```


