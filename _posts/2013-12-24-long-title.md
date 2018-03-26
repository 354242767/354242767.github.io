---
title:  CSS 布局解决方案（终结版)
date: 2018-03-22 23:31:06
categories:
- 前端
tags:
- CSS
---

# 前言

前端布局非常重要的一环就是页面框架的搭建，也是最基础的一环。在页面框架的搭建之中，又有居中布局、多列布局以及全局布局，今天我们就来总结总结前端干货中的CSS布局。

# 正文
## 居中布局
### 水平居中
#### 1）使用inline-block+text-align
##### 原理

- 先将子框由块级元素改变为行内块元素，再通过设置行内块元素居中以达到水平居中。

##### 用法

- 对子框设置display:inline-block，对父框设置text-align:center。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.child{
    display:inline-block;
}
.parent{
    text-align:center;
}

{% endhighlight %}

##### 优缺点

- 优点:兼容性好，甚至可以兼容ie6、ie7
- 缺点:child里的文字也会水平居中，可以在.child添加text-align:left;还原

### 垂直居中

#后记

#原文出处
