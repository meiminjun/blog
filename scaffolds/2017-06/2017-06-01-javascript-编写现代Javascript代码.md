title: javascript深入浅出系列-es6-编写现代Javascript代码
date: 2017-06-01 19:20:13
tags:
  - javascript
  - es-2015
  - linter
---

原文： https://dev.to/scastiel/writing-modern-javascript-code

# 编写现代Javascript代码

记得以前Javascript还处于是一种改变页面元素的语言？这些日子已经过去了，每种语言随着时间的推移而发展，我们使用它们也是如此，看看你一两年前写的代码：你不感到羞愧吗？如果是，这篇帖子就是写给你的
🙂

在这篇文章里，我会尝试这里列出一些很好的做法，使您的JavaScript代码更容易编写，阅读和维护

# 使用可以格式化代码的linter

第一个建议是使用一个代码linter,他会检查你的每一行代码是否遵守统一规则，特别是几个开发人员协同开发一个项目的时候：缩减，括号中的空格，将==替换为===...

但更重要的是，尽可能让您的linter自动修复您的代码。 ESLint非常好（使用--fix选项），它与所有主要的IDE集成，可以在保存时自动修复文件。

您也可以使用更为专注于格式化的“漂亮”，而不是检查，但结果基本相同😉

下一点将帮助你选择你的linter使用的规则:

# 为你的linter使用现代规则

如果您想知道您的代码需要什么规则，这里有一个提示:StandardJS. 
这是一个非常严格的linter,不会在规则中给您任何选择，但是它们中的每一个都越来越被社区所承认。下面是一些例子:

* 使用2空格缩进(我曾经使用4个空格,但实际上使用2是相当不错)
* 没有分号
* 在关键字(如if)和花括号后加空格
* and [a lot more](https://standardjs.com/rules-zhcn.html).

# 使用ES2015 +新特性

如果你用JavaScript开发,你还没有听说过ES2015 +(或ES6 ES7…)特性。这是不可或缺的了:

* 箭头函数：编写函数可以像 x => x * 2 是非常有用的函数式编程
* 类：停止使用原型函数，类更酷（但是不要滥用,JavaScript比任何面向对象的语言都要好得多）
* 使用数组和对象进行操作

```
function doSomething() {
  const a = doSomethingElse()
  const b = doSomethingWithA(a)
  const otherResults = { c: '😺', d: '🐶' }
  return { a, b, ...otherResults } // 相当于 { a: a, b: b，c: '😺', d: '🐶' }
}
const { a, c, ...rest } = doSomething() // 同样适用于数组
// `rest` 相当于 { b: ..., d: '🐶' }
```

* 使用更容易的使用的async/await:

```
async function doSomething() {
  const a = await getValueForA()
  const b = await getValueForBFromA(a)
  const [c, d] = await Promise.all([
    // parallel execution
    getValueForC(), getValueForDFromB(b)
  ])
  const total = await calculateTotal(a, b, c, d)
  return total / 1000
}
```

我们怎样使用这些特性呢？我的一篇文章给你一些建议（顺便说一下,与最新版本的Node.js,你可能不需要babel就可以使用最新的一些特性）

# 使用函数式编程

现在，函数式编程已经取得了很大的成功，不仅仅是在JavaScript中。这是什么原因呢?它使代码更加可预测、更安全、更确定，并且在使用时更容易维护。以下是一些简单的建议:

首先，停止使用for循环，在大多数情况下你不需要他们，例如：

```
const arr = [{ name: 'first', value: 13 }, { name: 'second', value: 7 }]

// 以前:
const res = {}
for (let i = 0; i < arr.length; i++) {
  const calculatedValue = arr[i].value * 10
  if (calculatedValue > 100) {
    res[arr[i].name] = calculatedValue
  }
}

// 更好:
const res = arr
  .map(elem => ({ name: elem.name, calculatedValue: elem.value * 10 }))
  .filter(elem => elem.calculatedValue > 100)
  .reduce((acc, elem) => ({
    [elem.name]: calculatedValue,
    ...acc
  }), {})
```

好吧，我承认这是一个非常极端的例子，如果你不经常使用函数式编程的情况下，他看起来会非常的复杂，也许我们可以这样简化一下：

```
const enrichElementWithCalculatedValue =
  elem => ({ name: elem.name, calculatedValue: elem.value * 10 })
const filterElementsByValue = value =>
  elem => elem.calculatedValue > value
const aggregateElementInObject = (acc, elem) => ({
  [elem.name]: calculatedValue,
  ...acc
})
const res = arr
  .map(enrichElementWithCalculatedValue)
  .filter(filterElementsByValue(100))
  .reduce(aggregateElementInObject, {})
```

这里我们定义了三个函数基本上就是它们的名字

第二:创建局部函数(即使是在现有函数中)，无需注释就可以记录代码。

注意，三个局部函数不修改它们执行的上下文。没有外部变量被修改,没有被其他方法被调用，
他们称为纯函数在函数式编程中。他们有一些巨大的优势:

* 它们是易测试的，因为从给定的参数来说，只有一个可能的结果，即使我们把函数多调用几次;
* 无论应用程序的实际状态如何，它们都可以提供相同的结果;
* 在函数调用之前和之后，应用程序状态保持不变。

所以我的第三条建议是:多使用纯函数!

# 最后还有一些其他的建议

* 经常使用异步代码，多使用promise，查看带有[RxJS](http://reactivex.io/rxjs/)的观察效果([有一个关于函数编程的很好的教程，可以测试你的函数式编程](http://reactivex.io/learnrx/))
* 编写测试代码!应该是显而易见的，但是我知道很多项目都有未经测试的代码，尽管测试JavaScript(前端或后端)并不像看起来那么困难。
* 使用语言的新特性：例如停止使用`arr.indexOf(elem) !== -1` 赞成使用`arr.includes(elem)`
* 多阅读技术文章：[JavaScript subreddit](https://www.reddit.com/r/javascript/)是了解生态系统中最酷的实践的一个很好的来源
* 哦，最后，我能给你最好的建议是：总是重构你的代码！改进你一年前写的模块？借此机会使用`const`代替`var`，使用`箭头函数`或者`async/await`来简化代码...总之用最好的代码进行工作!😉


