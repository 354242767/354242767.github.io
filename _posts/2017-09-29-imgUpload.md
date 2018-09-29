---
title: 图片上传中文件处理
date: 2017-09-29 23:31:30
categories:
- 前端
tags:
- JavaScript
- HTML
- 图片上传
description:
 本篇幅主要概述图片上传过程的处理操作，包括：DataURL与File,Blob,canvas对象之间的互相转换，以及canvas的图片压缩技术。
 
---

# 不同图像对象间的相互转换

## File/Blob对象转换为dataURL
**File对象也是一个Blob对象(多一个文件名属性)，二者的处理相同。**
``` html
    function blobToDataURL(blob, callback) {
        var a = new FileReader();
        a.onload = function(e) {callback(e.target.result);};
        a.readAsDataURL(blob);
    }
    //example:
    blobToDataURL(blob, function (dataurl){
        console.log(dataurl);
    });
    blobToDataURL(file, function (dataurl){
        console.log(dataurl);
    });

 

```


## dataURL转换为File/Blob对象
``` html
    function dataURLtoBlob(dataurl) {
        var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
            bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
        while(n--){
            u8arr[n] = bstr.charCodeAt(n);
        }
        return new Blob([u8arr], {type:mime});
    }

    function dataURLtoFile(dataurl, filename) {
        var arr = dataurl.split(','), mime = arr[0].match(/:(.*?);/)[1],
            bstr = atob(arr[1]), n = bstr.length, u8arr = new Uint8Array(n);
        while(n--){
            u8arr[n] = bstr.charCodeAt(n);
        }
        return new File([u8arr], filename, {type:mime});
    }
    //test:
    var blob = dataURLtoBlob('data:text/plain;base64,YWFhYWFhYQ==');
    var file = dataURLtoFile('data:text/plain;base64,YWFhYWFhYQ==', 'test.png');

 
```

## dataURL图片数据绘制到canvas
**先构造Image对象，src为dataURL，图片onload之后绘制到canvas**
``` html
    function dataUrlToCanvas(dataurl){
        var img = new Image();
        img.src = dataurl;
        var canvas = document.createElement("canvas");  
        img.onload = function(){
            var ctx = canvas.getContext('2d'); 
            canvas.width = image.width;  
            canvas.height = image.height;  
            ctx.drawImage(image, 0, 0, canvas.width, canvas.height); 
        
        };
        return canvas;
    }
    

```

## File/Blob的图片文件数据绘制到canvas
**先使用上述blobToDataURL方法将File/Blob->dataUrl,在使用上述dataUrlToCanvas->canvas**
``` html
    function blobToCanvas(bolb){
        var dataurl =   blobToDataURL(blob, function (dataurl){
                            return dataurl;
                        });
        dataUrlToCanvas(dataurl);
    }
```

## canvas转换为dataURL (从canvas获取dataURL)
``` html
    var dataurl = canvas.toDataURL('image/png');
    var dataurl2 = canvas.toDataURL('image/jpeg', 0.8);//质量压缩
```

# 图片压缩上传
1. 思路：file/bolb对象 -> dataurl(base64) ->(尺寸压缩) canvas -> (质量压缩)dataurl(base64) -> file/bolb对象 ->     ajax通过FormData对象上传blob/file文件(前端压缩上传/后台压缩不做赘述)

2. 代码

``` html
    var canvas = blobToCanvas(bolb);
    var dataurl =  canvas.toDataURL('image/jpeg', 0.8);
    var file = dataURLtoFile(dataurl, 'test.png');

    //使用ajax发送
    var fd = new FormData();
    fd.append("image", file);
    var xhr = new XMLHttpRequest();
    xhr.open('POST', '/server', true);
    xhr.send(fd);

```