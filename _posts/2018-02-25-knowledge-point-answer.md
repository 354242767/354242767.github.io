---
title: 前端面试知识点总结(答案)
date: 2018-02-25 00:23:23
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
- <!doctype html>声明位于文档中的最前面的位置，处于 `<html>` 标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。
- 在HTML与CSS标准确定之后，浏览器一方面要按照标准去实现对HTML与CSS的支持，另一方面又要保证对非标准的旧网页设计的后向兼容     性。因此，现代的浏览器一般都有两种渲染模式：标准模式和怪异模式。

3. **渐进增强（progressive enhancement）、优雅降级（graceful degradation）**
- 渐进增强：先针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

4. **怎样理解 HTML 语义化**
- 语义化是指根据内容的结构化（内容语义化），选择合适的标签（代码语义化），便于开发者阅读和写出更优雅的代码的同时，让浏览器的爬虫和机器很好的解析。
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
- meta 元素可提供有关页面的元信息(meta-information),比如针对搜索引擎和更新频度的描述和关键词。
- 必需的属性：content—定义与 http-equiv 或 name 属性相关的元信息。
- 可选的属性：http-equiv—把 content 属性关联到 HTTP 头部；name—把 content 属性关联到一个名称；scheme——定义用于翻译 content 属性值的格式。                 

7. **行内标签 和 块级标签**
- 行内类型：标签的大小由标签的内容决定，不能设置width和height，不会自动换行。(a、span、lebal、img)
- 块级标签：可以设置width和height，会自动换行。(div、p、h1~6、ul、ol、li、dl、dt、dd)
- display可以改变元素的布局显示方式(inline、block、inline-block、table、table-cell..)

8. **data- 属性的好处**
- 自定义属性，HTML5中使用data-xxx用于数据的存放（可通过attribute方法进行存取、data-属性选择器获取）

### CSS篇
1. **盒模型 box-sizing**
- content-box：标准盒子模型，margin+border+padding+content(width)
- border-box:IE盒子模型，margin+content(width)

2. **CSS中的长度单位**
- `px`,`pt`,`rem`,`em`,`ex`,`vw`,`vh`,`vh`,`vmin`,`vmax`

3. **CSS 权重优先级**
- !important > 行内样式 > ID > 类、伪类、属性 > 标签名 > 继承 > 通配符 （就近原则）

4. **position的值**
- static（默认）：按照正常文档流进行排列；
- relative（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；
- absolute(绝对定位)：参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位；
- fixed(固定定位)：所固定的参照对像是可视窗口。

5. **display的常用值 和 作用**
- inline：行内（内联）显示，无法设置宽高（内容撑起）
- inline-block：行内块显示，可设置宽高
- block：块级显示，自动换行。
- none：此元素不会被显示。**元素display在 显示 和 none 之间切换时会dom树重排（布局变化）而visibility：hidden不会**
- （不常用）table、table-cell、table-row、list-item、etc.

6. **重绘和重排（回流）**
- 重绘（repaint）：元素外观的改变所触发的浏览器行为。 如：颜色、 visibility、背景色等。
- 回流(reflow)：元素的规模尺寸，布局，隐藏等改变而需要浏览器重新构建渲染树。
- 注意：回流必将引起重绘，而重绘不一定会引起回流。
- 优化:

7. **引发回流的操作**
- 页面渲染初始化
- 添加或者删除可见的DOM元素
- 元素位置改变
- 元素尺寸改变：边距、填充、边框、宽度和高度
- 内容改变:比如文本改变或者图片大小改变而引起的计算值宽度和高度改变
- 浏览器窗口尺寸改变——resize事件发生时
- 获取一些属性时(需要浏览器重新构建渲染树计算)：offsetxxx、scrollxxx、clientxxx、getComputedStyle() (currentStyle in IE)

8. **关于回流的优化**
- 集中读取引发回流的操作
- 善用文档片段createDocumentFragment()，避免多次构建渲染树。
- 利用diplay和float将回流控制在2次（先 隐藏/脱离文档流 再操作最后显示）

9. **link和@import引入css的区别**
- 从属关系：@import是 CSS 提供的语法规则，只有导入样式表的作用；link是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。
- 加载顺序：加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。
加载页面时，link标签引入的 CSS 被同时加载；@import引入的 CSS 将在页面加载完毕后被加载。
- 兼容性区别：@import是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link标签作为 HTML 元素，不存在兼容性问题。
- DOM可控性：可以通过 JS 操作 DOM ，插入link标签来改变样式；由于 DOM 方法是基于文档的，无法使用@import的方式插入样式。
- 权重：link引入的样式权重大于@import引入的样式。

10. 清除浮动的方法
- 添加空标签 clear：both
- 设置父元素 overflow：hidden（ie 还需触发haslayout ，zoom：1）实质是触发BFC 。
- 父元素浮动（不推荐 ，有时要浮动到body）
- 父元素设置 display:table（也是触发BFC）盒模型属性已经改变。
- 使用:after伪元素（联想css计数器、伪元素和伪类区别）

11. 什么是BFC
- BFC（block formatting context）：块级格式化上下文，默认情况下只有根元素（body)一个块级上下文。
- BFC的规则：
    1. BFC就是页面上的一个隔离的独立容器（block），容器里面的子元素不会影响到外面的元素。
    2. 计算BFC的宽高时，浮动元素也参与计算。
- BFC触发条件：
    1. float的值不为none
    2. overflow的值不为visible
    3. display的值为table-cell、tabble-caption和inline-block之一
    4. position的值不为static或则releative中的任何一个

12. **如何实现水平居中和垂直居中。**
- 水平居中
    1. 使用inline-block + text-align（对子框设置display:inline-block，对父框设置text-align:center。）
    2. 使用table + margin（对子框设置display:table，再设置margin:0 auto。）
    3. 使用定位 + transform（对父框position:relative，对子框position:absolute，left:50%，transform:translateX(-50%)。）
    4. 使用flex + margin（先将父框设置为display:flex，再设置子框margin:0 auto。）
    5. 使用flex + justify-content（先将父框设置为display:flex，再设置justify-content:center。）
- 垂直居中
    1. 使用table-cell + vertical-align（先将父框设置为display:table-cell，再设置vertical-align:middle）
    2. 使用absolute + transform（先将父框设置为position:relative，再设置子框position:absolute，top:50%，transform:translateY(-50%)。）
    3. 使用flex + align-items（先将父框设置为position:flex，再设置align-items:center。）

13. **解释一下css3的flexbox，以及适用场景**
- 它是CSS3新增的一种布局模式。该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。
- 这种布局方式在条目尺寸未知或动态时也能工作（移动端也有很好的体验）。

14. **两栏布局实现**
- 左栏width已知：左栏浮动，右栏margin
- 左栏width未知：左栏浮动，右栏overfllow（触发BFC）
- 左右行内块（width百分比/右margin+右width: calc(100% - 左width)）
- 左右浮动（同上）
- flex布局（父元素display:flex ;左栏flex: 0 0 auto;右栏flex: 0 0 auto;）
- grid方案（父元素display:gird+grid-template-columns: 120px 1fr;左栏grid-column: 1;右栏grid-column: 2;）
- 多栏布局在以上基础上同理

15. **流式布局、自适应布局、响应式布局**
- 静态布局： 固定尺寸样式的布局方式（px）。
- 流式布局：屏幕分辨率变化时，页面里元素的大小会变化而但布局不变。
    1. 实现方式：百分比宽+px高
    2. 缺点：屏幕太大或者太小都会导致元素无法正常显示
- 自适应布局：屏幕分辨率变化时，页面里面元素的位置会变化而大小不会变化。
    1. 实现方式： @media 媒体查询给不同尺寸和介质的设备切换不同的样式。
    2. 缺点：媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。
- 响应式布局：不同屏幕分辨率下布局样式不同，即元素位置和大小都会变。
    1. 实现方式： @media 媒体查询给不同尺寸和介质的设备切换不同的样式。
    2. 缺点：媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。
    3. 优点：适应pc和移动端

16. **移动端布局方案**
- 响应式布局、rem、flex布局等等具体根据应用场景。

17. **常遇到的浏览器兼容性问题有哪些？常用的hack的技巧**
- 不同浏览器的标签默认margin和padding不同（*{ margin: 0; padding: 0;}）
- IE6双边距bug：块属性标签float之后，又有横向的margin值，在IE6中显示会比设置的大（在float标签样式控制中加入display:inline;）
- 设置较小的高度标签（一般小于10px），在IE6，IE7中超出自己设置的高度（overflow:hidden;或者line-height 小于你设置的高度。）
- 浏览器样式识别规则不同
    1. 不同版本（ie）：渐进识别的方式，从总体中逐渐排除局部（如background->.background:\9->+background->_background）
    2. 不同版本（ie）：IE条件注释法(`<!--[if IE]>ie识别<![endif]-->`、 `<!--[if gte IE 6]>ie6以上版本识别<![endif]` )
    3. 不同内核：浏览器前缀渐进增强的方式 （如-webkit-xxx -> -moz-xxx -> -o-xxx -> xxx;反之优雅降级）

18. **简述一下src与href的区别**
- src用于替换当前元素，href用于在当前文档和引用资源之间确立联系。
- `<script src='xxx.js'></script>` 当浏览器解析到该元素时，会暂停浏览器的渲染，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。
- `<link href='xxx.css' rel='stylesheet'/>` 浏览器会识别该文档为css文件，就会并行下载资源并且不会停止对当前文档的处理。这也是为什么建议使用link方式来加载css，而不是使用@import方式。

19. **CSS3新特性**
- `过渡`、 `动画`、`转换`、`选择器`、`阴影`、`边框`、`背景`、`反射`、`文字`、`颜色`、`渐变`、`滤镜`、`弹性布局`、`栅格布局`、`多列布局`、`媒体查询`、`混合模式`。

20. **CSS优化**
- 选择器性能：避免层级或过度限制css、避免使用通配符或隐式通配符、避免使用后代选择器、尽量使用最具体的类别
- 加载性能：避免import 、减少文件体积（压缩）、减少请求次数（css合并、sprite）、减少阻塞加载、提高并发
- 渲染性能：css放在head中，减少repaint和reflow；合理利用 GPU 加速；CSS 动画实现方式；最优layout 策略选择；减少页面渲染 junky
- 可维护性、健壮性：合理命名、抽象复用、合理的结构层次；OOCSS思想

### JavaScript篇
1. **对JavaScript语言的理解**
- JavaScript是一种专为与网页交互而设计的脚步语言，有ECMAScript、Dom、Bom三个部分组成
    1. ECMAScript：有ECMA-262定义，提供JavaScript的核心语言功能；
    2. Dom（文档对象模型）：提供访问和操作网页内容的方法和接口；
    3. Bom（浏览器对象模型）：提供与浏览器交互的方法和接口。

2. **js的基本类型有哪些？引用类型有哪些？null和undefined的区别**
- 基本类型：`Null`、`Undifined`、`Number`、`String`、`Boolean`5种。
- 复杂类型：`Object`、`Array`、


