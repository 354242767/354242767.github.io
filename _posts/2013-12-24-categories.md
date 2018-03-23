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
    typeof num, //
    typeof str, 
    typeof bool, 
    typeof und, 
    typeof nul, 
    typeof arr, 
    typeof json, 
    typeof fn, 
    typeof date, 
    typeof reg, 
    typeof error
 ); 
{% endhighlight %}

从输出的结果来看：
- number, string, boolean, function, undefined类型可以被准确判断出来
- 而null,arr, json, nul, date, reg, error 全部被检测为object类型.
- 故typeof操作符只适用于不包含Null这一类型的基本类型的判断,而不适用于复杂数据类型（Function除外）
