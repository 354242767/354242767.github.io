---
title:  CSS 布局解决方案（终结版)
date: 2018-03-22 23:31:06
categories:
- 前端
tags:
- CSS
description: 前端布局非常重要的一环就是页面框架的搭建，也是最基础的一环。在页面框架的搭建之中，又有居中布局、多列布局以及全局布局，今天我们就来总结总结前端干货中的CSS布局。
---


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

#### 2）使用table+margin
##### 原理

- 先将子框设置为块级表格来显示（类似 <table>），再设置子框居中以达到水平居中。

##### 用法

- 对子框设置display:table，再设置margin:0 auto。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.child {
    display:table;
    margin:0 auto;
}

{% endhighlight %}

##### 优缺点

- 优点:只设置了child，ie8以上都支持
- 缺点:不支持ie6、ie7,将div换成table

#### 3）使用table+margin
##### 原理

- 将子框设置为绝对定位，移动子框，使子框左侧距离相对框左侧边框的距离为相对框宽度的一半，再通过向左移动子框的一半宽度以达到水平居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。

##### 用法

- 对父框设置position:relative，对子框设置position:absolute，left:50%，transform:translateX(-50%)。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    position:relative;
}
.child {
    position:absolute;
    left:50%;
    transform:translateX(-50%);
}
{% endhighlight %}

##### 优缺点

- 优点:居中元素不会对其他的产生影响
- 缺点:transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀

#### 4）使用flex+margin
##### 原理

- 通过CSS3中的布局利器flex将子框转换为flex item，再设置子框居中以达到居中。

##### 用法

- 先将父框设置为display:flex，再设置子框margin:0 auto。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
}
.child {
    margin:0 auto;
}
{% endhighlight %}

##### 优缺点

- 优点:-
- 缺点:低版本浏览器(ie6 ie7 ie8)不支持

#### 5）使用flex+justify-content
##### 原理

- 通过CSS3中的布局利器flex中的justify-content属性来达到水平居中。

##### 用法

- 先将父框设置为display:flex，再设置justify-content:center。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
    justify-content:center;
}
{% endhighlight %}

##### 优缺点

- 优点:设置parent即可
- 缺点:低版本浏览器(ie6 ie7 ie8)不支持


### 垂直居中
#### 1）使用table-cell+vertical-align
##### 原理

- 通过将父框转化为一个表格单元格显示（类似 <td> 和 <th>），再通过设置属性，使表格单元格内容垂直居中以达到垂直居中。

##### 用法

- 先将父框设置为display:table-cell，再设置vertical-align:middle。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    display:table-cell;
    vertical-align:middle;
}
{% endhighlight %}

##### 优缺点

- 优点:兼容性较好，ie8以上均支持
- 缺点:不支持ie6、ie7,将div换成table

#### 2）使用absolute+transform
##### 原理

- 类似于水平居中时的absolute+transform原理。将子框设置为绝对定位，移动子框，使子框上边距离相对框上边边框的距离为相对框高度的一半，再通过向上移动子框的一半高度以达到垂直居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。

##### 用法

- 先将父框设置为position:relative，再设置子框position:absolute，top:50%，transform:translateY(-50%)。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    position:relative;
}
.child {
    position:absolute;
    top:50%;
    transform:translateY(-50%);
}
{% endhighlight %}

##### 优缺点

- 优点:居中元素不会对其他的产生影响
- 缺点:transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀


#### 3）使用flex+align-items
##### 原理

- 通过设置CSS3中的布局利器flex中的属性align-times，使子框垂直居中。

##### 用法

- 先将父框设置为position:flex，再设置align-items:center。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    position:flex;
    align-items:center;
}
{% endhighlight %}

##### 优缺点

- 优点:只设置parent
- 缺点:兼容性存在一定问题

### 水平垂直居中
#### 1）使用absolute+transform
##### 原理

- 将水平居中时的absolute+transform和垂直居中时的absolute+transform相结合。

##### 用法

- 详见：水平居中的3）和垂直居中的2）。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    position:relative;
}
.child {
    position:absolute;
    left:50%;
    top:50%;
    transform:tranplate(-50%,-50%);
}
{% endhighlight %}

##### 优缺点

- 优点:child元素不会对其他元素产生影响
- 缺点:兼容性存在一定问题

#### 2）使用inline-block+text-align+table-cell+vertical-align
##### 原理

- 使用inline-block+text-align水平居中，再用table-cell+vertical-align垂直居中，将二者结合起来。

##### 用法

- 详见：见水平居中的1）和垂直居中的1）。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    text-align:center;
    display:table-cell;
    vertical-align:middle;
}
.child {
    display:inline-block;
}
{% endhighlight %}

##### 优缺点

- 优点:兼容性较好
- 缺点:-

#### 3）使用flex+justify-content+align-items
##### 原理

- 通过设置CSS3布局利器flex中的justify-content和align-items，从而达到水平垂直居中。
##### 用法

- 详见：水平居中的4）和垂直居中的3）。

##### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="child>DEMO</div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
    justify-content:center;
    align-items:center;
}
{% endhighlight %}

##### 优缺点

- 优点:只设置了parent
- 缺点:兼容性存在一定问题

### 多列布局
#### 定宽+自适应
##### 1）使用float+overflow
###### 原理

- 通过将左边框脱离文本流，设置右边规定当内容溢出元素框时发生的事情以达到多列布局。

###### 用法

- 先将左框设置为float:left、width、margin-left，再设置实际的右框overflow:hidden。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.left {
    float:left;
    width:100px;
    margin-right:20px;
}
.right {
    overflow:hidden;
}
{% endhighlight %}

###### 优缺点

- 优点:简单
- 缺点:不支持ie6

##### 2）使用float+margin
###### 原理

- 通过将左框脱离文本流，加上右框向右移动一定的距离，以达到视觉上的多列布局。

###### 用法

- 先将左框设置为float:left、margin-left，再设置右框margin-left。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.left {
    float:left;
    width:100px;
}
.right {
    margin-left:120px;
}
{% endhighlight %}

###### 优缺点

- 优点:简单，易理解
- 缺点:兼容性存在一定问题，ie6下有3px的bug。right下的p清除浮动将产生bug

##### 3）使用float+margin（改良版）
###### 原理

- 在2）的基础之上，通过向右框添加一个父框，再加上设置左、右父框属性使之产生BFC以去除bug。

###### 用法

- 先将左框设置为float:left、margin-left、position:relative，再设置右父框float:right、width:100%、margin-left，最后设置实际的右框margin-left。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="rigth-fix">
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</div>

CSS
--------------------------------------
.left {
    float:left;
    width:100px;
    position:relative;
}
.right-fix {
    float:right;
    width:100%;
    margin-left:-100px;
}
.right {
    margin-left:120px;
}
{% endhighlight %}

###### 优缺点

- 优点:简单，易理解
- 缺点:-

##### 4）使用table
###### 原理

- 通过将父框设置为表格，将左右边框转化为类似于同一行的td，从而达到多列布局。

###### 用法

- 先将父框设置为display:table、width:100%、table-layout:fixed，再设置左右框display:table-cell，最后设置左框width、padding-right。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.parent {
    display:table;
    width:100%;
    table-layout:fixed;
}
.left {
    width:100px;
    padding-right:20px;
}
.right,.left {
    display:table-cell;    
}
{% endhighlight %}

###### 优缺点

- 优点:简单，易理解
- 缺点:div变为table

##### 5）使用flex
###### 原理

- 通过设置CSS3布局利器flex中的flex属性以达到多列布局。

###### 用法

- 先将父框设置为display:flex，再设置左框flex:1，最后设置左框width、margin-right。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
}
.left {
    width:100px;
    margin-right:20px;
}
.right {
    flex:1;
}

{% endhighlight %}

###### 优缺点

- 优点:flex很强大
- 缺点:兼容性存在一定问题，性能存在一定问题

#### 两列定宽+一列自适应
##### 1）使用float+overflow
###### 原理

- 这种情况与两列定宽查不多。

###### 用法

- 先将左、中框设置为float:left、width、margin-right，再设置右框overflow:hidden。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="center">
        <p>center</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
}
.left {
    width:100px;
    margin-right:20px;
}
.right {
    flex:1;
}

{% endhighlight %}

###### 优缺点

- 优点:-
- 缺点:-

#### 不定宽+自适应
##### 1）使用float+overflow
###### 原理

- 这种情况与两列定宽查不多。

###### 用法

- 先将左框设置为float:left、margin-right，再设置右框overflow: hidden，最后设置左框中的内容width。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.left{
        float: left;
        margin-right: 20px;
    }
.right{
    overflow: hidden;
}
.left p{
    width: 200px;
}

{% endhighlight %}

###### 优缺点

- 优点:简单
- 缺点:ie6下兼容性存在一定问题

##### 2）使用table
###### 原理

- 通过将父框改变为表格，将左右框转换为类似于同一行的td以达到多列布局，设置父框宽度100%，给左框子元素一个固定宽度从而达到自适应。

###### 用法

- 先将父框设置为display: table、width: 100%，再设置左、右框display: table-cell，最后设置左框width: 0.1%、padding-right以及左框中的内容width。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.parent{
    display: table; width: 100%;
    }
.left,.right{
    display: table-cell;
}
.left{
    width: 0.1%;
    padding-right: 20px;
}
.left p{
    width:200px;
}

{% endhighlight %}

###### 优缺点

- 优点:简单，易理解
- 缺点:ie6 ie7不支持

##### 3）使用flex
###### 原理

- 通过设置CSS3布局利器flex中的flex属性以达到多列布局，加上给左框中的内容定宽、给右框设置flex达到不定款+自适应。

###### 用法

- 先将父框设置为display:flex，再设置右框flex:1，最后设置左框margin-right:20px、左框中的内容width。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.parent {
    display:flex;
}
.left {
    margin-right:20px;
}
.right {
    flex:1;
}
.left p{
    width: 200px;
}

{% endhighlight %}

###### 优缺点

- 优点:flex很强大
- 缺点:兼容性存在一定问题，性能存在一定问题

#### 两列不定宽+一列自适应
##### 3）使用float+overflow
###### 原理

- 这个情况与一列不定宽+一列自适应查不多。

###### 用法

- 先将左、中框设置为float:left、margin-right，再设置右框overflow:hidden，最后给左中框中的内容设置width。

###### 代码实例

{% highlight r%}
HTML
--------------------------------------
<div class="parent">
    <div class="left">
        <p>left</p>
    </div>
    <div class="center">
        <p>center</p>
    </div>
    <div class="right">
        <p>right</p>
        <p>right</p>
    </div>
</div>

CSS
--------------------------------------
.left,.center{
    float: left;
    margin-right: 20px;
}
.right{
    overflow: hidden;
}
.left p,.center p{
    width: 100px;
}

{% endhighlight %}

###### 优缺点

- 优点:-
- 缺点:-

### 等分布局

![Caption](http://ww3.sinaimg.cn/mw690/81b78497jw1emfgwjrh2pj21hc0u01g3.jpg)

公式转化:

l = w * n + g * (n-1) -> l = w * n + g * n – g -> l + g = （w + g） * n










#后记

#原文出处
