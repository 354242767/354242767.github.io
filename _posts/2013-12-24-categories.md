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

{% highlight r %}
 var num = new Number(1);
 var str = new String('hello world');
 var boolean = new Boolean(true);
{% endhighlight %}

## 3.constructor

在使用instanceof操作符时，我们无法检测出num，str，和bool的类型，但constructor却可以。

constructor本来是原型对象上的属性，指向构造函数。但是根据实例对象寻找属性的顺序，若实例对象上没有实例属性或方法时，就去原型链上寻找，因此，实例对象也是能使用constructor属性的。

我们先来输出一下num.constructor的内容，即数字类型的变量的构造函数是什么样子的：

{% highlight console %}
 ƒ Number() { [native code] } 
{% endhighlight %}

我们可以看到它指向了Number的构造函数，因此，我们可以使用num.constructor==Number来判断num是不是Number类型的，其他的变量也类似：

{% highlight r %}
 console.log(
    //null和undifined 没有 constructor属性
    //以下结果均为true
    num.constructor==Number,
    str.constructor==String,
    bool.constructor==Boolean,
    arr.constructor==Array,
    json.constructor==Object,
    fn.constructor==Function,
    date.constructor==Date,
    reg.constructor==RegExp,
    error.constructor==Error
 ); 

不过constructor也不是保险的，因为constructor属性是可以被修改的，会导致检测出的结果不正确，例如：
{% highlight r %}
function Person(){}
function Student(){}
Student.prototype = new Person();
var John = new Student();

console.log(John.constructor==Student); // false
console.log(John.constructor==Person);  // true
{% endhighlight %}

在上面的例子中，Student原型中的constructor被修改为指向到Person，导致检测不出实例对象John真实的构造函数。

同时，使用instaceof和construcor,被判断的array必须是在当前页面声明的！比如，一个页面（父页面）有一个框架，框架中引用了一个页面（子页面），在子页面中声明了一个array，并将其赋值给父页面的一个变量，这时判断该变量，Array == object.constructor;会返回false；
原因：
1、array属于引用型数据，在传递过程中，仅仅是引用地址的传递。
2、每个页面的Array原生对象所引用的地址是不一样的，在子页面声明的array，所对应的构造函数，是子页面的Array对象；父页面来进行判断，使用的Array并不等于子页面的Array；切记，不然很难跟踪问题！

## 4.使用Object.prototype.toString.call
{% highlight r %}
console.log(
    Object.prototype.toString.call(num),
    Object.prototype.toString.call(str),
    Object.prototype.toString.call(bool),
    Object.prototype.toString.call(arr),
    Object.prototype.toString.call(json),
    Object.prototype.toString.call(fn),
    Object.prototype.toString.call(und),
    Object.prototype.toString.call(nul),
    Object.prototype.toString.call(date),
    Object.prototype.toString.call(reg),
    Object.prototype.toString.call(error)
);
//'[object Number]' '[object String]' '[object Boolean]' '[object Array]' '[object Object]'
//'[object Function]' '[object Undefined]' '[object Null]''[object Date]' '[object RegExp]'
//'[object Error]'
{% endhighlight %}

从输出的结果来看，Object.prototype.toString.call(变量)输出的是一个字符串，字符串里有一个数组，第一个参数是Object，第二个参数就是这个变量的类型，而且，所有变量的类型都检测出来了，我们只需要取出第二个参数即可。或者可以使用Object.prototype.toString.call(arr)=="object Array"来检测变量arr是不是数组。