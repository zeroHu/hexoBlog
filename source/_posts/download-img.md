---
title: download-img
date: 2017-11-29 11:47:48
tags: js 下载图片或者文件
---
#### 主要讲解用js下载文件或者图片
> 起因：因工作需要，用canvas画出了一张图片，图片格式是（base64).
```
base64图片转为blob文件

function dataURLtoBlob(dataurl) {
    var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
    while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
    }
    return new Blob([u8arr], { type: mime });
}

//**blob to dataURL**
function blobToDataURL(blob, callback) {
    var a = new FileReader();
    a.onload = function (e) { callback(e.target.result); };
    a.readAsDataURL(blob);
}

// 生成
var _file = dataURLtoBlob(imgbase64); // c就是base64字符串

//Blob_test();
function BlobDownload(){
    var blob;
    if(!window.Blob){
        console.log('不支持');
    }
    else{
        blob = _file;
        console.log('xxxxxxxxxxxx->',window.URL.createObjectURL(blob));
        if(window.URL){
            document.getElementById("download-btn").innerHTML = '<a download="invitationCard.jpg" href="' + window.URL.createObjectURL(blob) + '" target="_blank">下载邀请函图片</a>';
        }
    }
}
BlobDownload();
```