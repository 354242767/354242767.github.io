---
title: 脚本开发
date: 2021-02-24 18:44:22
categories:
- 前端
tags:
- javaScript
description: 
- 怎么样去开发一个简单的chrome浏览器插件，（抢票抢鞋脚本开发）
---

### chrome浏览器插件的目录结构

``` html
|-- _locales
|  |-- en
|  |  |-- messages.json
|  |-- zh-CN
|  |  |-- messages.json
|  |-- zh-TW
|  |  |-- messages.json
|-- html
|-- |-- test.html
|-- image
|-- |-- icon.png
|-- manifest.json
|-- script
|-- |-- test.js
```
- html:存放html页面
- js :存放js
- image ：初期图标(可无)
- manifest ：核心入口文件

### 写一个manifest.json

``` html
{
  "name": "chrome插件",
  "version": "0.0.1",
  "manifest_version": 2,

  // 简单描述
  "description": "chrome plug",
  "icons": {
    "16": "image/icon16.png",
    "48": "image/icon48.png"
  },
  // 选择默认语言
  "default_locale": "en",

  // 浏览器小图表部分
  "browser_action": {
    "default_title": "反劫持",
    "default_icon": "image/icon.png",
    "default_popup": "html/test.html"
  },

  // 引入一个脚本
  "content_scripts": [
    {
      "js": ["script/test.js"],
      // 在什么情况下使用该脚本
      "matches": [
        "http://*/*",
        "https://*/*"
      ],
      // 什么情况下运行【文档加载开始】
      "run_at": "document_start"
    }
  ],
  // 应用协议页面
  "permissions": [
    "http://*/*",
    "https://*/*"
  ]
}
```
### 抢购脚本步骤
``` html
setIntervel(function(){
  if(Date.now()>new Date('活动时间')){
    //登陆的用户信息cookie。userInfo等
    document.getElementById('xxx').click();
    //验证码取值
    let vaildateValue=document.getElementById('xxx').innerHtml();
    //验证码填值 
    getElementById('xxx').value = vaildateValue;
    //验证码提交
    
  }
},100);
```

— 可参考vue-devtools插件


