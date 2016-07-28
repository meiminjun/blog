title: 浅谈javacript 笔记系列--- 继承与原型链
date: 2016-07-26 18:57:13
categories:
  - javascript
tags:
  - javascript
---

# [继承与原型链](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain#使用_class_关键字)

对于那些熟悉基于类的面向对象语言（Java 或者 C++）的开发者来说，JavaScript 的语法是比较怪异的，这是由于 JavaScript 是一门动态语言，而且它没有类的概念（ ES6 新增了class 关键字，但只是语法糖，JavaScript 仍旧是基于原型）。

涉及到继承这一块，Javascript 只有一种结构，那就是：对象。在 javaScript 中，每个对象都有一个指向它的原型（prototype）对象的内部链接。这个原型对象又有自己的原型，直到某个对象的原型为 null 为止（也就是不再有原型指向），组成这条链的最后一环。这种一级一级的链结构就称为原型链（prototype chain）。

虽然，原型继承经常被视作 JavaScript 的一个弱点，但事实上，原型继承模型比经典的继承模型更强大。尽管在原型模型上构建一个标准的类模型是相当琐碎的，但如果采取其他方式实现的话会更加困难。

<!-- more -->

## javascript 之 原型继承

原型继承是让父对象作为子对象的原型，从而达到继承的目的：

```
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
// 要继承的父对象
var parent = {
  name: "Papa"
};
// 新对象
var child = object(parent);
// 测试
console.log(child.name); // "Papa"

// 父构造函数
function Person() {
  // an "own" property
  this.name = "Adam";
}
// 给原型添加新属性
Person.prototype.getName = function () {    return this.name;};

// 创建新person
var papa = new Person();

// 继承
var kid = object(papa);
console.log(kid.getName()); // "Adam"

// 父构造函数
function Person() { 
   // an "own" property  
     this.name = "Adam";
 }

// 给原型添加新属性
 Person.prototype.getName = function () {    return this.name;};
 
 // 继承
 var kid = object(Person.prototype);
 console.log(typeof kid.getName); // "function",因为是在原型里定义的
 console.log(typeof kid.name);  // "undefined", 因为只继承了原型
```

同时，ECMAScript5也提供了类似的一个方法叫做Object.create用于继承对象，用法如下：
```
/* 使用新版的ECMAScript 5提供的功能 */
var child = Object.create(parent);
var child = Object.create(parent, { 
   age: { value: 2} // ECMA5 descriptor
   });
console.log(child.hasOwnProperty("age")); // true
```

而且，也可以更细粒度地在第二个参数上定义属性：





```
function A(a){
  this.varA = a;
}

// 以上函数 A 的定义中，既然 A.prototype.varA 总是会被 this.varA 遮蔽，
// 那么将 varA 加入到原型（prototype）中的目的是什么？
A.prototype = {
  varA : null,  // 既然它没有任何作用，干嘛不将 varA 从原型（prototype）去掉？
      // 也许作为一种在隐藏类中优化分配空间的考虑？
      // https://developers.google.com/speed/articles/optimizing-javascript#Initializing instance variables
      // 将会验证如果 varA 在每个实例不被特别初始化会是什么情况。
  doSomething : function(){
    console.log(11123);
  }
}

function B(a, b){
  A.call(this, a);
  this.varB = b;
}
B.prototype = Object.create(A.prototype, {
  varB : {
    value: null, 
    enumerable: true, 
    configurable: true, 
    writable: true 
  },
  doSomething : { 
    value: function(){ // override
      A.prototype.doSomething.apply(this, arguments); // call super
      // ...
    },
    enumerable: true,
    configurable: true, 
    writable: true
  }
});
B.prototype.constructor = B;

var b = new B();
b.doSomething();

console.log(b);
```

## javascript 之 类继承(构造函数继承)示例

```
//Shape - superclass
function Shape() {
  this.x = 0;
  this.y = 0;
}

Shape.prototype.move = function(x, y) {
    this.x += x;
    this.y += y;
    console.info("Shape moved.");
};

// Rectangle - subclass
function Rectangle() {
  Shape.call(this); //call super constructor.
}

Rectangle.prototype = Object.create(Shape.prototype);

var rect = new Rectangle();

rect instanceof Rectangle //true.
rect instanceof Shape //true.

rect.move(1, 1); //Outputs, "Shape moved."

```


深入理解继承：

参考：深入理解JavaScript系列（46）：代码复用模式（推荐篇）

* http://www.ituring.com.cn/article/56184

阮一峰之面向对象：

* [Javascript 面向对象编程（一）：封装](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_encapsulation.html)

* [Javascript面向对象编程（二）：构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)

* [Javascript面向对象编程（三）：非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)
