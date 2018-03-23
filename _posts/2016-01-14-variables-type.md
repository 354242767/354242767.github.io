---
title: 如何确定一个变量的类型
date: 2016-01-14 23:30:09
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

{% highlight r %}
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
{% endhighlight %}

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

我们现在再来看看ECMA里是是怎么定义Object.prototype.toString.call的：
{% highlight r%}
Object.prototype.toString() When the toString method is called, the following steps are taken:
1. Get the [[Class]] property of this object.
2. Compute a string value by concatenating the three strings"[object", Result (1), and "]".
3. Return Result (2)
{% endhighlight %}

上面的规范定义了Object.prototype.toString的行为：首先，取得对象的一个内部属性[[Class]]，然后依据这个属性，返回一个类似于"[object Array]"的字符串作为结果（看过ECMA标准的应该都知道，[[]]用来表示语言内部用到的、外部不可直接访问的属性，称为“内部属性”）。利用这个方法，再配合call，我们可以取得任何对象的内部属性[[Class]]，然后把类型检测转化为字符串比较，以达到我们的目的。

## 5.jquery中$.type的实现
在jquery中提供了一个$.type的接口，来让我们检测变量的类型：

{% highlight r %}
console.log(
    $.type(num),
    $.type(str),
    $.type(bool),
    $.type(arr),
    $.type(json),
    $.type(func),
    $.type(und),
    $.type(nul),
    $.type(date),
    $.type(reg),
    $.type(error)
);
// number string boolean array object function undefined null date regexp error
{% endhighlight %}

看到输出结果，有没有一种熟悉的感觉？对，他就是上面使用Object.prototype.toString.call(变量)输出的结果的第二个参数呀。

我们这里先来对比一下上面所有方法检测出的结果，横排是使用的检测方法， 竖排是各个变量：

    type   | typeof | instanceof | constructor | toString.call | $.type
    num    | number    | false | true | [object Number]    | number
    str    | string    | false | true | [object String]    | string
    bool   | boolean   | false | true | [object Boolean]   | boolean
    und    | undefined | false | -    | [object Undefined] | undefined
    nul    | object    | false | -    | [object Null]      | null
    arr    | object    | true  | true | [object Array]     | array
    json   | object    | true  | true | [object Object]    | object
    fn     | function  | true  | true | [object Function]  | function
    date   | object    | true  | true | [object Date]      | date
    reg    | object    | true  | true | [object Regexp]    | regexp
    error  | object    | true  | true | [object Error]     | error
    优点 |使用简单，能直接输出结果|能检测出复杂的类型|基本能检测出所有的类型|检测出所有的类型| -
    缺点 |检测出的类型太少|基本类型检测不出，且不能跨iframe|不能跨iframe，且constructor易被修改|IE6下undefined,null均为Object| -


这样对比一下，就更能看到各个方法之间的区别了，而且Object.prototype.toString.call和$type输出的结果真的很像。我们来看看jquery（2.1.2版本）内部是怎么实现$.type方法的：

{% highlight r %}
// 实例对象是能直接使用原型链上的方法的
var class2type = {};
var toString = class2type.toString;

// 省略部分代码...

type: function( obj ) {
    if ( obj == null ) {
        return obj + "";
    }
    // Support: Android<4.0, iOS<6 (functionish RegExp)
    return (typeof obj === "object" || typeof obj === "function") ?
        (class2type[ toString.call(obj) ] || "object") :
        typeof obj;
},

// 省略部分代码... 

// Populate the class2type map
jQuery.each("Boolean Number String Function Array Date RegExp Object Error".split(" "), function(i, name) {
    class2type[ "[object " + name + "]" ] = name.toLowerCase();
});
{% endhighlight %}

我们先来看看jQuery.each的这部分：

{% highlight r %}
// Populate the class2type map
jQuery.each("Boolean Number String Function Array Date RegExp Object Error".split(" "), function(i, name) {
    class2type[ "[object " + name + "]" ] = name.toLowerCase();
});

//循环之后，`class2type`的值是： 
class2type = {
    '[object Boolean]' : 'boolean', 
    '[object Number]'  : 'number',
    '[object String]'  : 'string',
    '[object Function]': 'function',
    '[object Array]'   : 'array',
    '[object Date]'    : 'date',
    '[object RegExp]'  : 'regExp',
    '[object Object]'  : 'object',
    '[object Error]'   : 'error'
}
{% endhighlight %}

再来看看type方法：

{% highlight r %}
// type的实现
type: function( obj ) {
    // 若传入的是null或undefined，则直接返回这个对象的字符串
    // 即若传入的对象obj是undefined，则返回"undefined"
    if ( obj == null ) {
        return obj + "";
    }
    // Support: Android<4.0, iOS<6 (functionish RegExp)
    // 低版本regExp返回function类型；高版本已修正，返回object类型
    // 若使用typeof检测出的obj类型是object或function，则返回class2type的值，否则返回typeof检测的类型
    return (typeof obj === "object" || typeof obj === "function") ?
        (class2type[ toString.call(obj) ] || "object") :
        typeof obj;
}
{% endhighlight %}
当typeof obj === "object" || typeof obj === "function"时，就返回class2type[ toString.call(obj)。到这儿，我们就应该明白为什么Object.prototype.toString.call和$.type那么像了吧，其实jquery中就是用Object.prototype.toString.call实现的，把'[object Boolean]'类型转成'boolean'类型并返回。若class2type存储的没有这个变量的类型，那就返回"object"。
除了"object"和"function"类型，其他的类型则使用typeof进行检测。即number, string, boolean类型的变量，使用typeof即可。

