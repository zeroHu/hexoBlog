---
title: 获取图片的原始高度宽度和获取图片的平均色值
date: 2018-09-03 15:36:19
tags: javascript
---
#### 获取图片的原始宽高度

> html结构

```html
<img id="image_id" src="" alt="">
<div class="color-end" style="width:200px;height:200px;border:1px solid #000;"></div>
```


```javascript
function getImgWidthHeight() {
  var img = new Image();
  img.addEventListener('load', function () {
    console.log('-----', img.width, img.height, img.naturalWidth, img.naturalHeight);
    // if need color
    // var canvas = document.createElement('canvas');
    // getImageColor(canvas, img); 
  }, false);
  img.src = 'https://static-image.xfz.cn/1535618935_589.jpg' + '?' + new Date().getTime();
  img.setAttribute('crossOrigin', '');
}
```

#### 获取图片的平均色值

```javascript
function getImageColor(canvas, img) {
      canvas.width = img.width;
      canvas.height = img.height;

      var context = canvas.getContext("2d");

      context.drawImage(img, 0, 0);

      // 获取像素数据
      var data = context.getImageData(0, 0, img.width, img.height).data;
      
      var r = 0;
      var g = 0;
      var b = 0;

      // 取所有像素的平均值
      for (var row = 0; row < img.height; row++) {
        for (var col = 0; col < img.width; col++) {
          r += data[((img.width * row) + col) * 4];
          g += data[((img.width * row) + col) * 4 + 1];
          b += data[((img.width * row) + col) * 4 + 2];
        }
      }

      // 求取平均值
      r /= (img.width * img.height);
      g /= (img.width * img.height);
      b /= (img.width * img.height);

      // 将最终的值取整
      r = Math.round(r);
      g = Math.round(g);
      b = Math.round(b); 

      var str = "rgb(" + r + "," + g + "," + b + ")";
      console.log('======str', str)
      // $('.color-end').css('background', str);
}
```