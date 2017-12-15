---
title: canvas
date: 2017-07-10 22:57:22
tags: canvas
---
### canvas
#### canvas 知识点总结
> 文本样式

```javascript
var canvas = document.getElementById('canvasId').getContext("2d");
canvas.fillStyle = "#3e454c";
canvas.font = `${that.date.fontsize}px serif`;
```
> fillText 文本居中

```javascript
canvas.textAlign = "center";
//that.canvas.width 指的是定义的canvas宽度大小 可以获取 可以直接设值
canvas.fillText(name, this.canvas.width/2, that.name.top);
```
> 图片base64地址获取

```javascript
//在全部画完之后
var canvas  = document.getElementById('canvasId');
var imgbase64 = canvas.toDataURL("image/jpeg", 1);//只有jpeg压缩有效果
var imgbase64 = canvas.toDataURL("image/png", 1);//这样压缩无效果
var imgbase64 = canvas.toDataURL();//不指定图片类型，不压缩
```
> 文本折行 回车\n 能够折行的效果

```javascript
var introcontent = content.split('\n');
var addHeight = 0;
//处理\n
introcontent.forEach(function(val,firstindex){
    if(firstindex == 0){
        addHeight = 0;
    }else{
        //获取addHeight值
        var textFnArr = that.textBranch(codeid, introcontent[firstindex-1], that.text.maxWidth);
        textFnArr.forEach(function(word, index){
            if(index == textFnArr.length-1){
                addHeight += that.text.lineHeight*(textFnArr.length);
            }
        });
    }
    //处理折行
    //textBranch 值 codeid 是canvasId号，写入的文本内容，文本最大宽度
    that.textBranch(codeid, introcontent[firstindex], that.text.maxWidth).forEach(function(word, index){
        //fillText参数 ： text , x , y
        canvas.fillText(word, that.text.left, that.text.lineHeight * index + that.text.top + addHeight);
    });
});
// 文本换行
textBranch(codeid, text, width, font) {
    var that = this;
    var canvas = document.getElementById(codeid);
    var context = canvas.getContext('2d');
    var result = [];
    var breakPoint = 0;
    while ((breakPoint = findBreakPoint(text, width, context)) !== -1) {
        result.push(text.substr(0, breakPoint));
        text = text.substr(breakPoint);
    }
    if (text) {
        result.push(text);
    }
    return result;

    // 计算字符
    function findBreakPoint(text, width, context){
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
}
```
