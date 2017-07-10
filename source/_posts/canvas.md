---
title: canvas
date: 2017-07-10 22:57:22
tags: canvas
---
### canvas
#### canvas 导入图片 导出图片
```html
<!doctype html>
<html>

<head>
    <meta charset="UTF-8">
    <title>插入图片</title>
    <style type="text/css">
    body {
        background: #fff;
    }
    
    #oc {
        background: #ccc;
    }
    </style>
    <script type="text/javascript">
    window.onload = function() {
        var Oc = document.getElementById("oc");
        var Gc = Oc.getContext("2d");
        var yImg = new Image();
        // yImg.crossOrigin = "Anonymous";

        yImg.src = "./888.png";
        yImg.onload = function() {
            draw(this);

            // 导出图片
            var canvas = document.getElementById('oc');
            var dataURL = canvas.toDataURL();
            console.log('dataurl', dataURL);
            var imgResult = document.createElement('img')
            imgResult.src = dataURL;
            document.getElementById('div1').appendChild(imgResult)

        };

        function draw(obj) {
            Gc.drawImage(obj, 0, 0, 148, 62); //插入图片
            // 给某一个区域插入背景图片,并设置平铺方式
            var bg = Gc.createPattern(obj, "repeat");
            Gc.fillStyle = bg;
            Gc.fillRect(0, 0, 200, 200);
        };

    }
    </script>
</head>

<body>
    <canvas id="oc" width="400" height="400">
        <span>不支持canvas的浏览器</span>
    </canvas>
    <div id="div1"></div>
</body>

</html>
```
