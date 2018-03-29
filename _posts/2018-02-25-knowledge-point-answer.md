---
title: 前端面试知识点总结(答案)
date: 2018-03-25 00:23:23
categories:
- 前端
tags:
- 面试
description:
- 总结2018前端关注的知识点，整理自己前端的知识体系。
---

### HTML篇
1. HTML、XML、XHTML 有什么区别
- HTML：超文本标记语言，语法较为松散，不严格的web语言；标签可以不闭合，不区分大小写。
- XML：可扩展标记语言，主要用于存储数据和结构，可以自由创建标签；标签必须闭合，严格区分大小写。
- XHTML：可扩展超文本标记语言，相较HTML语法更加严格。标签必须闭合，标签必须小写。

2. 文档声明的作用?标准模式和怪诞模式的区别
- <!doctype html>声明位于文档中的最前面的位置，处于 <html> 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。
- 在HTML与CSS标准确定之后，浏览器一方面要按照标准去实现对HTML与CSS的支持，另一方面又要保证对非标准的旧网页设计的后向兼容性。因此，现代的浏览器一般都有两种渲染模式：标准模式和怪异模式。

3. 怎样理解 HTML 语义化
- 语义化是指根据内容的结构化（内容语义化），选择合适的标签（代码语义化），便于开发者阅读和写出更优雅的代码的同时，让浏览器的爬虫和机器很好的解析。
- 语义化的好处是：
    1. 有利于SEO，有助于爬虫抓取更多的有效信息，爬虫是依赖于标签来确定上下文和各个关键字的权重。
    2. 语义化的HTML在没有CSS的情况下也能呈现较好的内容结构与代码结构
    3. 方便其他设备的解析
    4. 便于团队开发和维护

4. HTML5新特性
- HTML5 新元素
    `nav`，`header`，`footer`，`artical`，`section`，`aside`，`canvas`，`details`，`mark`，`audio`，`video`。
- HTML5 表单
- HTML5 Canvas绘图
HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

```javascript

var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");
ctx.fillStyle="#FF0000";
ctx.fillRect(0,0,150,75);

```
- HTML5 拖放
<dl>
    <dt>拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。</dt>
    <dd>拖动什么 - ondragstart 和 setData()</dd>
    <dd>放到何处 - ondragover</dd>
    <dd>进行放置 - ondrop</dd>
</dl>

```html

<img draggable="true" ondragstart="drag(event)" ondragover="allowDrop(event)" ondrop="drop(event)"/>

```

```javascript

function allowDrop(ev){
    ev.preventDefault();
}

function drag(ev){
    ev.dataTransfer.setData("Text",ev.target.id);   
}

function drop(ev){
    ev.preventDefault();
    var data=ev.dataTransfer.getData("Text");
    ev.target.appendChild(document.getElementById(data));
}


```
