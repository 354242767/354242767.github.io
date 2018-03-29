---
title: 前端面试知识点总结(答案)
date: 2018-03-25 00:23:23
categories:
- 前端
tags:
- 面试
- HTML
- CSS
- JavaScript
description:
- 总结2018前端关注的知识点，整理自己前端的知识体系。
---

### HTML篇
1. **HTML、XML、XHTML 有什么区别**
- HTML：超文本标记语言，语法较为松散，不严格的web语言；标签可以不闭合，不区分大小写。
- XML：可扩展标记语言，主要用于存储数据和结构，可以自由创建标签；标签必须闭合，严格区分大小写。
- XHTML：可扩展超文本标记语言，相较HTML语法更加严格。标签必须闭合，标签必须小写。

2. **文档声明的作用?标准模式和怪诞模式的区别**
- <!doctype html>声明位于文档中的最前面的位置，处于 <html> 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。
- 在HTML与CSS标准确定之后，浏览器一方面要按照标准去实现对HTML与CSS的支持，另一方面又要保证对非标准的旧网页设计的后向兼容     性。因此，现代的浏览器一般都有两种渲染模式：标准模式和怪异模式。

3. **渐进增强（progressive enhancement）、优雅降级（graceful degradation）**
- 渐进增强：先针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

4. **怎样理解 HTML 语义化**
- 语义化是指根据内容的结构化（内容语义化），选择合适的标签（代码语义化），便于开发者阅读和写出更优雅的代码的同时，让浏览器的   爬虫和机器很好的解析。
- 语义化的好处是：
    1. 有利于SEO，有助于爬虫抓取更多的有效信息，爬虫是依赖于标签来确定上下文和各个关键字的权重。
    2. 语义化的HTML在没有CSS的情况下也能呈现较好的内容结构与代码结构
    3. 方便其他设备的解析
    4. 便于团队开发和维护

5. **HTML5 新特性**
- HTML5 新元素
- HTML5 Input
- HTML5 Canvas绘图
- HTML5 拖放
- HTML5 地理定位
- HTML5 Audio(音频)、Video(视频)
- HTML5 Web存储(localStorage)、(sessionStorage)
- HTML5 应用缓存
- HTML5 Web Workers
- HTML5 服务器发送事件（server-sent event）

6. **mata 标签**
- <meta> 元素可提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。
- 必需的属性：content——定义与 http-equiv 或 name 属性相关的元信息。
- 可选的属性：http-equiv——把 content 属性关联到 HTTP 头部；name——把 content 属性关联到一个名称；scheme——定义用于翻译 content 属性值的格式。                 

7. **行内标签 和 块级标签**
- 行内类型：标签的大小由标签的内容决定，不能设置width和height，不会自动换行。(a、span、lebal、img)
- 块级标签：可以设置width和height，会自动换行。(div、p、h1~6、ul、ol、li、dl、dt、dd)
- display可以改变元素的布局显示方式(inline、block、inline-block、table、table-cell..)

8. **data- 属性的好处**
- 自定义属性，HTML5中使用data-xxx用于数据的存放（可通过attribute方法进行存取、data-属性选择器获取）

### CSS篇
