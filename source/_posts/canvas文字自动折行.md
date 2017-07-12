---
title: canvas文字自动折行
date: 2017-07-12 14:32:19
tags: canvas fillText
---
```html
<html>

<head>
    <title>canvas demo</title>
    <style>
    body {
        padding: 20px;
        background: #eee;
    }
    
    #canvas {
        border: 1px solid #ccc;
    }
    </style>
</head>

<body>
    <canvas id="canvas" width="300" height="400" />
    <script>
    function findBreakPoint(text, width, context) {
        var min = 0;
        var max = text.length - 1;

        while (min <= max) {
            var middle = Math.floor((min + max) / 2);
            var middleWidth = context.measureText(text.substr(0, middle)).width;
            var oneCharWiderThanMiddleWidth = context.measureText(text.substr(0, middle + 1)).width;
            if (middleWidth <= width && oneCharWiderThanMiddleWidth > width) {
                return middle;
            }
            if (middleWidth < width) {
                min = middle + 1;
            } else {
                max = middle - 1;
            }
        }

        return -1;
    }

    function breakLinesForCanvas(text, width, font) {
        var canvas = document.getElementById('canvas');
        var context = canvas.getContext('2d');
        var result = [];
        var breakPoint = 0;

        if (font) {
            context.font = font;
        }

        while ((breakPoint = findBreakPoint(text, width, context)) !== -1) {
            result.push(text.substr(0, breakPoint));
            text = text.substr(breakPoint);
        }

        if (text) {
            result.push(text);
        }

        return result;
    }

    var result = breakLinesForCanvas('使用很寻常的二分查找，如果某一个位置之前的文字宽度小于等于设定的宽度，并且它之后一个字之前的文字宽度大于设定的宽度，那么这个位置就是文本的换行点。上面只是找到一个换行点，对于输入的一段文本，需要循环查找，直到不存在这样的换行点为止, 完整的代码如下', 300, '16px 微软雅黑');

    var lineHeight = 30;
    var context = document.getElementById('canvas').getContext('2d');
    context.font = "16px 微软雅黑";

    result.forEach(function(line, index) {
        context.fillText(line, 0, lineHeight * index + 30);
    });
    </script>
</body>

</html>

```
