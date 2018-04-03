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
- 总结2018前端关注的知识点，整理自己前端的知识体系。不定时更新
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
- 优化:见8

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

10. **清除浮动的方法**
- 添加空标签 clear：both
- 设置父元素 overflow：hidden（ie 还需触发haslayout ，zoom：1）实质是触发BFC 。
- 父元素浮动（不推荐 ，有时要浮动到body）
- 父元素设置 display:table（也是触发BFC）盒模型属性已经改变。
- 使用:after伪元素（联想css计数器、伪元素和伪类区别）

11. **什么是BFC**
- BFC（block formatting context）：块级格式化上下文，默认情况下只有根元素（body)一个块级上下文。
- BFC的规则：
    1. BFC就是页面上的一个隔离的独立容器（block），容器里面的子元素不会影响到外面的元素。
    2. 计算BFC的宽高时，左右浮动元素和子浮动元素也参与计算。
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
- 以上方式涉及兼容问题，具体选择看情况

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
    * 实现方式：百分比宽+px高
    * 缺点：屏幕太大或者太小都会导致元素无法正常显示
- 自适应布局：屏幕分辨率变化时，页面里面元素的位置会变化而大小不会变化。
    * 实现方式： @media 媒体查询给不同尺寸和介质的设备切换不同的样式。
    * 缺点：媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。
- 响应式布局：不同屏幕分辨率下布局样式不同，即元素位置和大小都会变。
    * 实现方式： @media 媒体查询给不同尺寸和介质的设备切换不同的样式。
    * 缺点：媒体查询是有限的，也就是可以枚举出来的，只能适应主流的宽高。
    * 优点：适应pc和移动端

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
- JavaScript是一种专为与网页交互而设计的脚步语言，由ECMAScript、Dom、Bom三个部分组成
    1. ECMAScript：有ECMA-262定义，提供JavaScript的核心语言功能；
    2. Dom（文档对象模型）：提供访问和操作网页内容的方法和接口；
    3. Bom（浏览器对象模型）：提供与浏览器交互的方法和接口。

2. **js的基本类型有哪些？引用类型有哪些？null和undefined的区别**
- 基本类型：`Null`、`Undifined`、`Number`、`String`、`Boolean`5种。
- 引用类型：`Object`（`Array`、`Date`、`Function`、`Regexp`、`Error`)。
- Null：空对象指针，特殊对象（正常或意料之中的值的空缺）；Undifined：声明但未赋值/初始化（出乎意料或错误的值的空缺）

3. **引用类型和基本类型区别**
- 基本类型的值内存大小固定保存在栈内存中
- 引用类型的值保存在堆内存中
- 包含引用类型值的变量实际包含的是指向该对象的指针，而不是对象本身
- 一个变量到另一个变量复制，会创建这个值的副本（引用对象则复制的是指针）
- 确定基本数据类型使用 typeof 操作符，确定引用数据类型使用 instanceof 操作符（扩展见4类型判断的方法）

4. **简述类型判断的方法有哪些**
- typeof操作符：能检测基本数据类型（Function也可以）
- intanceof操作符：能检测复杂数据类型
- Constructor属性：除Null和Undefined没有该属性外都能检测出数据类型
- Object.prototype.toString.call()方法:能检测出所有类型
- $.type()方法：底层实现同上，能检测出所有类型

5. **常用的dom操作API**
- 创建：createElement()、createTextNode()、cloneNode()、createDocumentFragment()
- 添加：appendChild()、insertBefore()、replaceChild()
- 删除：removeChild()
- 查询：getElementById()、getElementsByTagName()、getElementsByName()、getElementsByClassName()、querySelector()、        querySelectorAll()

6. **事件冒泡和事件捕获**
- js事件流的三个阶段分别为：捕获、目标、冒泡
    1. 捕获：事件由页面元素接收，逐级向下，到具体的元素  
    2. 目标：具体的元素本身  
    3. 冒泡：跟捕获相反，具体元素本身触发，逐级向上，到页面元素 

7. **事件委托**
- 利用事件冒泡将可能发生在子元素上的事件绑定在父元素上，再根据具体触发事件的元素执行相应的操作。
- 优点：减少事件注册，节省内存；动态添加事件（新添加的子元素也能触发）
- 缺点：基于事件冒泡的兼容性。

8. **对闭包的理解**
- 不要单纯的就闭包的定义而解释（如仅回答：可以读取函数内部的变量，让这些变量的值始终保持在内存中。）
- 拓展：理解闭包->理解作用域（局部/全局变量访问权限,作用域呈层级包含状态，形成作用域链）->可以阻止变量被 GC 回收(js的两种垃圾回收方式标记清除和引用计数)

9. **对this的理解**
- this是在运行时基于函数的执行环境绑定的
    1. 函数作为变量出现（非属性），this指向Global对象（严格模式undefined）
    2. 函数作为对象方法调用，this指向调用对象（使用call、apply、bind时将this指向第一个参数）
    3. 构造函数中的this指向新创建的对象。
    4. ES6 箭头函数内的this值继承自外围作用域。

10. **call，apply，bind**
- 用于指定this的环境，第一个参数即为推送的指向
- obj.bind(newObj)返回的是函数,按需调用obj.bind(newObj)()的方式
- obj.call(newObj,arg1,arg2)立即调用，后续参数以列表方式
- obj.call(newObj,arr)立即调用，后续参数以数组方式

11. **创建对象的常用方式**
- 构造函数方式 var o=new Object();/var p=new Person('cxh')。缺点是方法无复用，每个对象的方法重新创建，浪费内存 
- 对象字面量方式 var o={name:'cxh'}。缺点是同类型对象创建繁琐
- 工厂函数方式 creatObj(a,b,c){var o=new Object();xxx;retturn o;}。缺点是无法判确定回对象类型
- 原型方式 function Person(){};Person.prototype.xxx=xxx。缺点是不灵活
- 构造函数+原型方式 （最佳实践）

12. **实现继承的多种方式**
- 原型继承
- 构造函数实现继承
- 组合式继承
- 寄生组合式继承
- es6中的class

13. **new 一个对象具体做了什么**
- 创建一个新对象
- 新对象的_proto_属性指向构造函数的原型对象
- 将构造函数的作用域赋值给新对象（也所以this对象指向新对象）
- 执行构造函数内部的代码，将属性添加给新对象
- 返回新对象

14. **原生对象、宿主对象、自定义对象**
- JS中，可以将对象分为原生对象(内部对象)、宿主对象和自定义对象三种。
- 原生对象:js提供的对象（如：Object、Number、Boolean、Array等），可直接实例化。包含内置对象，内置对象在脚本程序初始化时被创建，  不必实例化（如Math、Date等）。
- 宿主对象：执行JS脚本的环境（如浏览器）提供的对象（window、document、history、etc.）。
- 自定义对象：开发者定义的对象（var Person=XXX）。
- 不建议对内置对象进行扩展:内置对象一般都提供了特定的方法，而且我们无法确定浏览器何时会实现与我们不一致的扩展。

15. **什么是“use strict”,好处和坏处**
- 严格模式是ES5引入的，更好的将错误检测引入代码的方法。顾名思义，这种模式使得Javascript在更严格的条件下运行。
- 优点：
    1. 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
    2. 消除代码运行的一些不安全之处，保证代码运行的安全；
    3. 提高编译器效率，增加运行速度；
    4. 为未来新版本的Javascript做好铺垫。
    5. 注：IE6,7,8,9 均不支持严格模式。
- 缺点：
    1. 禁用了一些功能（如：eval()、with(){}、delete操作等）。
    2. 变量必须先声明，再使用；属性不能重名。
    3. 不能修改arguments；不能在函数内定义arguments变量；不能使用arugment.caller和argument.callee。
    4. 如果你要引用匿名函数，需要对匿名函数命名。
    5. etc.

16. **js的作用域理解**
- 所有变量（基本和引用数据类型）都存在于一个执行环境（作用域）当中，这个执行环境决定了变量的生命周期，以及哪些代码可以访问其中的变量：
- 执行环境有全局执行环境和函数执行环境之分
- 执行流进入函数时，函数环境会被推入到环境栈中
- 每次进入新的执行环境，都会创建一个用于搜索变量和函数的作用域链
- 变量的执行环境有助于确定何时释放内存

17. **js变量提升**
- 答此问题需介绍js的语言特性：弱类型、动态的、解释型的脚本语言（了解不同语言特性见18）。-->js代码解析原则:第一个步骤是解释，第二个步骤是执行。 
- 所谓解释就是会先通篇扫描所有的Js代码，然后把所有声明提升到顶端（作用域）。执行（略）
- 然后介绍变量提升特点:只声明提升（栗子：console.log(a);var a=10;==>var a;console.log(a)//undefined;a=10）注:函数提升在变量提升之前。
    
18. **js语言特性**
- js的语言特性：弱类型、动态的、解释型的脚本语言
- 弱类型：类型检查不严格，偏向于容忍隐式类型转换。 
- 强类型：类型检查严格，偏向于不容忍隐式类型转换。 
- 动态类型：运行的时候执行类型检查。 
- 静态类型：编译的时候就知道每个变量的类型。 
- 解释型：程序不需要编译，程序在运行的时候才翻译成机器语言，每执行一次都要翻译一次，因此效率比较低，但是跨平台性好。 
- 编译型：程序在执行之前需要一个专门的翻译过程，把程序编译为机器语言的文件，运行时直接使用编译的结果就行了。 
- 标记语言：标记语言的存在就是用来被读取(浏览)的，而其本身是没有行为能力的，在标记语言里你会看到<和>这些尖括号，这是用来写出“层次”  和”属性”的，换句话说，它是被动的。并不具备与访问者互动的能力。 
- 编程语言：它是具有逻辑性和行为能力，这是主动的（说通俗一点，它是有思想的）。
- 脚本语言：它介于标记语言和编程语言之间，脚本语言不需要编译，可以直接用，由解释器来负责解释。

**js的多态**
- 面向对象的语言特点:封装、继承、多态
- 多态的基本概念：一个变量(含引用类型)在不同情况下的多种状态（弱类型语言天生多态，只有在赋值时才确认类型）。
- 实现多态的方式两种：
    1. 重写/覆盖:覆盖指子类重新定义父类方法，这正好就是基于prototype继承的用法
    2. 重载：重载是指多个同名但参数不同的方法（js语法特性不支持，会覆盖之前同名变量；但接受的参数是多态的）。

**js动画和css3动画比较**
- 功能涵盖面，JS比CSS3大
    - 定义动画过程的@keyframes不支持递归定义，如果有多种类似的动画过程，需要调节多个参数来生成的话，将会有很大的冗余（比如jQuery Mobile的动画方案），而JS则天然可以以一套函数实现多个不同的动画过程
    - 时间尺度上，@keyframes的动画粒度粗，而JS的动画粒度控制可以很细
    - CSS3动画里被支持的时间函数非常少，不够灵活
    - 以现有的接口，CSS3动画无法做到支持两个以上的状态转化
- 实现/重构难度不一，CSS3比JS更简单，性能调优方向固定
- 对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码
- CSS动画有天然事件支持（TransitionEnd、AnimationEnd，但是它们都需要针对浏览器加前缀），JS则需要自己写事件
- CSS3有兼容性问题，而JS大多时候没有兼容性问题
- CSS动画比JS流畅的前提：
    - 在Chromium基础上的浏览器中
    - JS在执行一些昂贵的任务
    - 同时CSS动画不触发layout或paint
    - 在CSS动画或JS动画触发了paint或layout时，需要main thread进行Layer树的重计算，这时CSS动画或JS动画都会阻塞后续操作。


**js常用字符串API、数组API**
- 字符串API：
    1. 不影响原字符串：
        - toString();
        - str.charAt(index)、str.charCodeAt(index)-->返回给定位置的那个字符、字符编码。
        - 去空格-str.trim()-->该方法删除前置和后缀的所有空格，然后返回结果。
        - 查询索引-str.indexOf(target,fromIndex)/lastIndexOf(target,fromIndex)-->从前往后搜索/从后往前搜索，返回index值。
        - 大小写转换-str.toLowerCase()/str.toUpperCase()、toLocaleLowerCase()/toLocaleUpperCase()
        - stringObject.replace(regexp/substr,replacement)
        - match() 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配
        - etc.
    2. 改变原字符串:
        - split() 方法用于把一个字符串分割成字符串数组。
- 数组API
    1. 不影响原数组：
        - concat():连接多个数组，返回新的数组
        - join()：将数组中所有元素以参数作为分隔符放入一个字符串
        - slice()：slice(start,end)，返回选定元素，左闭右开
        - map,filter,forEach,some,every用于迭代
        - 注：以上方法可用于字符串（join除外）
    2. 改变原数组：
        - unshift()/shift(): 添加/删除数组的第一个元素
        - push()/pop(): 添加/删除数组的最后一个元素
        - reverse(): 颠倒数组
        - sort(compare): 排序数组
        - splice(start,length,item): 删，增，替换数组元素，返回新数组

**深克隆实现**
- 需理解三个方面的知识：基本类型和引用类型的区别、如何判断一个变量的类型、递归实现

``` javascript
Object.prototype.clone = function(){
	if(this.constructor === Array||this.constructor === Object){
		var o = this.constructor === Array ? [] : {};
        for(var e in this){
            o[e] = typeof this[e] === "object" ? this[e].clone() : this[e];
        }
        return o;
	}else{
		return this;
	}
   
}
```

**ajax的理解**
- AJAX（Asynchronous JavaScript and XML）：在无需重新加载整个网页的情况下，能够更新部分网页。
- 核心是XMLHttpRequest对象
- 实现步骤
    1. 创建XMLHttpRequest对象xmlHttp -（该对象有两个方法open()/send()）
    2. 使用open()方法与服务器建立连接 - xmlHttp.open(method,url,true)，
        - 此步注意设置http的请求方式（post/get）,如果是POST方式，注意设置请求头信息xmlHttp.setRequestHeader("Content-Type","application/x-www-form-urlencoded")
    3. 向服务器端发送数据 - xmlHttp.send(null);如果是POST方式就不为空
    4. 在监听函数中针对不同的响应状态进行处理 -xmlHttp.onreadystatechange=function(){}
        - xmlHttp.readyState==4 //ajax已经完全接收了服务器的响应信息，但是状态码未必是正确的(0/1/2/3/4)
        - xmlHttp.status == 200 //成功(2xx/3xx/4xx/5xx)
        - xmlHttp.responseText/xmlHttp.requestXML 为服务器返回值
- 优缺点：
    - 优点：
        1. 异步通信，不阻塞页面，响应快，用户体验好。
        2. 减轻服务器负担，按需加载，节约带宽。
        3. 基于标准化并被广泛支持的技术，不需要下载插件或者小程序。
    - 缺点
        1. 破了浏览器的后退机制 - 无法返回上一部操作
        2. 安全问题 - 暴露更多数据和逻辑造成安全隐患（如跨站点脚步攻击、SQL注入攻击和基于credentials的安全漏洞等。）
        3. 对搜索引擎的支持比较弱。
        4. 兼容问题 -  并非所有端都支持（如一些手机和pad）
        5. 用户禁用js时，将无法获取数据

**js异常处理机制**
- 同其他后端语言类似：try-catch-finally
- js错误类型（内置对象）
    - Error：所有错误类型的父类型
    - EvalError、RangeError、SyntaxError、TypeError、URIError、ReferenceError
    - 可自定义错误类型：MyError.prototype = new xxxError();
- throw 关键字抛出来主动抛出异常 ：throw new Error(message);
- 不管是浏览器抛出的，还是代码主动抛出，都会让程序停止执行（try-catch处理的代码除外）。

**cookie、session、web storage**
- cookie：客户端数据持久化存储技术，小文本文件（大小限制单个cookie 4K），它可以包含有关用户的信息，伴随请求发送服务器（不安全）交互，http规范的一部分（不可或缺）
- session：会话级别的服务器存储技术，时间限制，占用服务器性能。
- web storage：本地数据存储，相比cookie容量更大，自带set/get方法，更为方便。localStorage和sessionStorage两种。

**websocket**
- WebSocket协议是基于TCP的一种新的网络协议。它实现了浏览器与服务器全双工(full-duplex)通信——允许服务器主动发送信息给客户端。
- 传统通信方式
    1. ajax轮询：需要服务器有很快的处理速度和资源。（速度）
    2. long poll：需要有很高的并发，也就是说同时接待客户的能力。（场地大小）
- 在HTML5中内置有一些API，用于响应应用程序发起的请求。
- 实现原理：在实现websocket连线过程中，需要通过浏览器发出websocket连线请求，然后服务器发出回应，这个过程通常称为“握手” 。在 WebSocket API，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。

**函数柯里化**
- 概念:是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。(头晕没怎么看明白..)
- 延迟计算、参数复用、动态生成函数的作用。
- 面试题辅助理解

``` javascript
//要求写一个函数add()，分别实现能如下效果：
add(1)(2)(3)(4)();//10
add(1,2)(3,4)();//10
add(1)(2)(3)(4);//10
add(1,2)(3,4);//10

function add(arg) {
    let sum = 0;
    sum = Array.prototype.slice.call(arguments).reduce((a,b) => {return a+b;},sum);
    var tmpf = function (tmarg) {
        if (arguments.length == 0) {
            return sum;
        }else{
            sum = Array.prototype.slice.call(arguments).reduce((a,b) => {return a+b;},sum);
            return tmpf;
        }
    };
    tmpf.toString = tmpf.valueOf = function () {
        return sum;
    }
    return tmpf;
}

```
**js的设计模式**
- 什么单列模式、工厂模式、代理模式、观察者模式之类的（共23种）。
- 高级程序员关注点。总的来说：是一套被反复使用、多数人知晓的、经过分类编目的、代码设计经验的总结。

**JS代码调试**
Chrome Developer Tool常用功能：
- 代码格式化：可以将被压缩的代码自动展开
- 实时代码编辑：可以在运行时动态改变 JS 代码，并且不需要刷新页面就可以看到效果，一般用这个实时的在代码里插 console.log
- DOM 事件/XHR 断点：可以针对 DOM 结构改变/属性改变/键盘鼠标事件 等下断点，直接断到事件的第一个 listener 函数上。还可以对 XHR 请求下断点，断到发起请求的那一行代码上
- 调用栈分析：这个非常常用，Scripts 面板下右上角的那一部分
- 自动异常断点：当代码执行出错时，可以自动断到出错的代码行上，直接分析出错时的运行时环境
- 分析 HTTP 请求：Network 面板下列出了所有的 HTTP 请求，可以很方便的查看请求内容、HTTP 头、请求时间等信息

**js优化**
- 可维护性：易于理解、可扩展、可调试
    1. 代码约定
    2. 松散耦合
- 性能
    1. 注意作用域
    2. 最小化语句数
    3. 选择正确方法
    4. 优化DOM交互
- 部署
    1. 构建过程
    2. 验证
    3. 压缩


### ES6

### Nodejs

### 计算机网络

### 浏览器相关

### 工程化

### 模块化

### 框架

### 数据结构

### 性能优化

### 其他


**以上内容为个人总结，如有错误敬请斧正**
