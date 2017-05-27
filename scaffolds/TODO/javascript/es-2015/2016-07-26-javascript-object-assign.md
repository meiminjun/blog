title: javascript深入浅出系列-Object 之 assign
date: 2016-07-26 09:57:14
categories:
  - javascript
tags:
  - javascript
  - es-2015
---

# javascript 之 object-assign 的方法介绍和示例

## [Object.assign()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

Object.assign() 方法可以把任意多个的源对象自身的可枚举属性拷贝给目标对象，然后返回目标对象。

### 语法

> Object.assign(target, ...sources)

target：目标对象。

sources：任意多个对象

### 返回值

目标对象会被返回。

### 描述

Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象身上。该方法使用源对象的 [ [ Get ] ] 和目标对象的 [ [ Set ] ]，所以它会调用相关 getter 和 setter。因此，它分配属性不仅仅是复制或定义新的属性。如果合并源包含了 getter，那么该方法就不适合将新属性合并到原型里。假如是拷贝属性定义到原型里，包括它们的可枚举性，那么应该使用 Object.getOwnPropertyDescriptor() 和 Object.defineProperty() 。

String类型和 Symbol 类型的属性都会被拷贝。

注意，在属性拷贝过程中可能会产生异常，比如目标对象的某个只读属性和源对象的某个属性同名，这时该方法会抛出一个 TypeError 异常，拷贝过程中断，已经拷贝成功的属性不会受到影响，还未拷贝的属性将不会再被拷贝。

> 注意， Object.assign 会跳过那些值为 null 或 undefined 的源对象。

<!-- more -->

### 示例

复制一个object

```
var obj = { a: 1 };
var copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }
```

合并 objects

```
var o1 = { a: 1 };
var o2 = { b: 2 };
var o3 = { c: 3 };

var obj = Object.assign(o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1);  // { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
```

继承属性和不可枚举属性是不能拷贝的

```
var obj = Object.create({foo: 1}, { // foo 是个继承属性。
    bar: {
        value: 2  // bar 是个不可枚举属性。
    },
    baz: {
        value: 3,
        enumerable: true  // baz 是个自身可枚举属性。
    }
});

var copy = Object.assign({}, obj);
console.log(copy); // { baz: 3 }
```

