---
title: 防抖节流实现
date: 2021-04-06 10:44:22
categories:
- 前端
tags:
- javaScript 
- 最佳实践
description: 
- 手写防抖节流函数
---

### 防抖(debounce)
#### 概念
  在第一次触发事件时，不立即执行函数，而是给出一个期限值
  - 如果在期限值内没有再次触发滚动事件，那么就执行函数
  - 如果在期限值内再次触发滚动事件，那么当前的计时取消，重新开始计时
``` javascript
function debounce(func, time) {
  let timer = null;
  return () => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, arguments);
    }, time);
  };
}

 ```
 ### 节流(throttle)
 #### 概念
 定期开放的函数，也就是让函数执行一次后，在某个时间段内暂时失效，过了这段时间后再重新激活
 
``` javascript
function throtte(func, time=1000) {
  let activeTime = 0;
  return () => {
    const current = Date.now();
    if (current - activeTime > time) {
      func.apply(this, arguments);
      activeTime = Date.now();
    }
  };
}
  
   ``` 
 
