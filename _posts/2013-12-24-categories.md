---
title: Categories
date: 2013-12-24 23:30:09
categories:
- Foo
- Bar
- Baz
---
在JavaScript中，有5种基本数据类型和1种复杂数据类型，基本数据类型有：Undefined, Null, Boolean, Number和String；复杂数据类型是Object，Object中还细分了很多具体的类型，比如：Array, Function, Date,Reg等等。今天我们就来探讨一下，使用什么方法判断一个出一个变量的类型。

首先,我们定义出js中几乎涉及到的所有变量类型以便于下文测试：
{% highlight r %}
 var num  = 1024;
 var str  = 'hello world';
 var bool = true;
 var und  = undefined;
 var nul  = null;
 var arr  = [1, 2, 3, 4];
 var json = {name:'cc', age:10};
 var fn = function(){ console.log('this is function'); }
 var date = new Date();
 var reg  = /^[a-zA-Z]{5,20}$/;
 var error= new Error();
{% endhighlight %}

## 1.typeof操作符

{% highlight r %}
console.log(
    typeof num,     //number
    typeof str,     //string
    typeof bool,    //boolean
    typeof und,     //undifined
    typeof nul,     //object
    typeof arr,     //object
    typeof json,    //object
    typeof fn,      //function
    typeof date,    //object
    typeof reg,     //object
    typeof error    //object
 ); 
{% endhighlight %}

从输出的结果来看：
- number, string, boolean, function, undefined类型可以被准确判断出来
- 而null,arr, json, nul, date, reg, error 全部被检测为object类型.
- 故typeof操作符只适用于不包含Null这一类型的基本类型的判断,而不适用于复杂数据类型（Function除外）

## 2.instanceof操作符

在 JavaScript 中，判断一个变量的类型尝尝会用 typeof 运算符，在使用 typeof 运算符时采用引用类型存储值会出现一个问题，无论引用的是什么类型的对象，它都返回 "object"。ECMAScript 引入了另一个 Java 运算符 instanceof 来解决这个问题。instanceof 运算符与 typeof 运算符相似，用于识别正在处理的对象的类型。

{% highlight r %}
 console.log(
    num instanceof Number,     
    str instanceof String,
    bool instanceof Boolean,
    und instanceof Object,
    nul instanceof Object,
    arr instanceof Array,
    json instanceof Object,
    fn instanceof Function,
    date instanceof Date,
    reg instanceof RegExp,
    error instanceof Error
 ); 
{% endhighlight %}

上述结果中，num,str,bool没有检测出类型，与 typeof 方法不同的是，instanceof 方法要求开发者明确地确认对象为某特定类型。如以下可以检测出类型：