title: javascript深入浅出系列-常用-数值判断
date: 2017-05-26 17:08:13
tags:
  - javascript
---

# JavaScript中检测数值的方法

## typeof(最常用)
在很多时候我们都需要对一个值进行判断，用的最多的就是typeof，而当判断array的时候，这个方法则不管用了

```
typeof [] // 'object'
```
> typeof 的返回值是个字符串哦

ps:以下typeof中是可用的判断类型

```
var a;
typeof a;				// "undefined"

a = "hello world";
typeof a;				// "string"

a = 42;
typeof a;				// "number"

a = true;
typeof a;				// "boolean"

a = null;
typeof a;				// "object" -- 奇怪的bug

a = undefined;
typeof a;				// "undefined"

a = { b: "c" };
typeof a;				// "object"
```

那么我们怎么去判断一个数组类型呢？

## instanceof操作符

这个操作符和JavaScript中面向对象有点关系，了解这个就先得了解JavaScript中的面向对象。因为这个操作符是检测对象的原型链是否指向构造函数的prototype对象的。

```
var arr = [1,2,3,1];     
alert(arr instanceof Array); // true  
```

## 对象的constructor属性

除了instanceof，每个对象还有constructor的属性，利用它似乎也能进行Array的判断。

```
var arr = [1,2,3,1];     
alert(arr.constructor === Array); // true  
```

第2种和第3种方法貌似无懈可击，但是实际上还是有些漏洞的，当你在多个frame中来回穿梭的时候，这两种方法就亚历山大了。由于每个iframe都有一套自己的执行环境，跨frame实例化的对象彼此是不共享原型链的，因此导致上述检测代码失效!

```
var iframe = document.createElement('iframe');   //创建iframe  
document.body.appendChild(iframe);   //添加到body中  
xArray = window.frames[window.frames.length-1].Array;     
var arr = new xArray(1,2,3); // 声明数组[1,2,3]     
  
alert(arr instanceof Array); // false     
  
alert(arr.constructor === Array); // false   
```

## 检测数组类型方法

以上那些方法看上去无懈可击，但是终究会有些问题，接下来向大家提供一些比较不错的方法，可以说是无懈可击了。

### Object.prototype.toString

Object.prototype.toString的行为：首先，取得对象的一个内部属性[[Class]]，然后依据这个属性，返回一个类似于"[object Array]"的字符串作为结果(看过ECMA标准的应该都知道，[[]]用来表示语言内部用到的、外部不可直接访问的属性，称为“内部属性”)。利用这 个方法，再配合call，我们可以取得任何对象的内部属性[[Class]]，然后把类型检测转化为字符串比较，以达到我们的目的。

```
function isArrayFn (o) {    
 return Object.prototype.toString.call(o) === '[object Array]';     
}  
var arr = [1,2,3,1];     
  
alert(isArrayFn(arr));// true   
```

call改变toString的this引用为待检测的对象，返回此对象的字符串表示，然后对比此字符串是否是'[object Array]'，以判断其是否是Array的实例。为什么不直接o.toString()?嗯，虽然Array继承自Object，也会有 toString方法，但是这个方法有可能会被改写而达不到我们的要求，而Object.prototype则是老虎的屁股，很少有人敢去碰它的，所以能一定程度保证其“纯洁性”：)

　　JavaScript 标准文档中定义: [[Class]] 的值只可能是下面字符串中的一个： Arguments, Array, Boolean, Date, Error, Function, JSON, Math, Number, Object, RegExp, String.
　　
　　
　　这种方法在识别内置对象时往往十分有用，但对于自定义对象请不要使用这种方法。
　　
### Array.isArray()


　　ECMAScript5将Array.isArray()正式引入JavaScript，目的就是准确地检测一个值是否为数组。IE9+、 Firefox 4+、Safari 5+、Opera 10.5+和Chrome都实现了这个方法。但是在IE8之前的版本是不支持的。

## 推荐

综合以上考虑，当前最佳方式：

```
var arr = [1,2,3,1];    
var arr2 = [{ abac : 1, abc : 2 }];    
  
function isArrayFn(value){  
    if (typeof Array.isArray === "function") {  
        return Array.isArray(value);      
    }else{  
        return Object.prototype.toString.call(value) === "[object Array]";      
    }  
}  
alert(isArrayFn(arr));// true   
alert(isArrayFn(arr2));// true   
```

## 判断JavaScript对象为null或者属性为空

首先说一下null 和 undefined 的区别

对已声明但未初始化的和未声明的变量执行typeof，都返回"undefined"

null表示一个空对象指针，typeof操作会返回"object"

一般不显式的把变量的值设置为undefined，但null相反，对于将要保存对象的变量，应明确的让该变量赋值为null值作为初始化变量。

```
var obj;
alert(obj);  //"undefined"
obj = null;
alert(typeof obj);  //"object"
alert(obj == null);  //true
bj = {};
alert(bj == null);  //false
```

下面是两个判断空对象的函数

1. 检查原型继承的

```
/*
 * 检测对象是否是空对象(不包含任何可读属性)。
 * 方法既检测对象本身的属性，也检测从原型继承的属性(因此没有使hasOwnProperty)。
 */
function isEmpty(obj)
{
    for (var name in obj) 
    {
        return false;
    }
    return true;
}
```

```
var a = {};
a.name = 'realwall';
console.log(isEmpty(a));  //false
console.log(isEmpty({}));  //true
console.log(isEmpty(null));  //true
//注意参数为null时无语法错误，即虽然不能对null空指针对象添加属性，但使用for in 语句
```

2. 不检查原型继承的

```
/*
 * 检测对象是否是空对象(不包含任何可读属性)。
 * 方法只既检测对象本身的属性，不检测从原型继承的属性。
 */
function isEmpty(obj)
{
    for(var name in obj)
    {
        if(obj.hasOwnProperty(name))
        {
            return false;
        }
    }
    return true;
};
```