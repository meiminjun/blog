title: 浅谈javacript 笔记系列--- 设计模式 之单例模式
date: 2016-06-11 11:57:13
categories:
  - javascript
tags:
  - javascript
  - 设计模式
---

# javascript设计模式之单例模式

## 定义和用法

在传统开发工程师眼里，单例就是保证一个类只有一个实例，实现的方法一般是先判断实例存在与否，如果存在直接返回，如果不存在就创建了再返回，这就确保了一个类只有一个实例对象。在JavaScript里，单例作为一个命名空间提供者，从全局命名空间里提供一个唯一的访问点来访问该对象。

## 正文

在JavaScript里，实现单例的方式有很多种，其中最简单的一个方式是使用对象字面量的方法，其字面量里可以包含大量的属性和方法：

``` bash
var mySingleton = {    
  property1: "something",
  property2: "something else",
  method1: function () {
      console.log('hello world');
  }
};

```

如果以后要扩展该对象，你可以添加自己的私有成员和方法，然后使用闭包在其内部封装这些变量和函数声明。只暴露你想暴露的public成员和方法，样例代码如下：

``` bash
var mySingleton = function() { /* 这里声明私有变量和方法 */
  var privateVariable = 'something private';

  function showPrivate() {
    console.log(privateVariable);
  } 
  /* 公有变量和方法（可以访问私有变量和方法） */
  return {
    publicMethod: function() {
      showPrivate();
    },
    publicVar: 'the public can see this!'
  };
};
var single = mySingleton();
single.publicMethod(); // 输出 'something private'
console.log(single.publicVar); // 输出 'the public can see this!'

```



## 如何拥有私有成员的单体

### 下划线标示法

```
var namespace = {};
namespace.DataParser = {
  _stripWhitespace:function(str) {
    return str.replace(/s+/,'');
  },
  _stringSplit:funtion(str,delimiter) {
    return str.split(delimiter);
  },
  //共有方法
  stringToArray:function(str,delimiter,stripWs) {
    if(stripWs) {
      str = this._stringWhitespace(str);
    }
    var outputArray = this._stringSplit(str,delimiter);
    return outputArray;
  }
}; 

```

### 使用闭包

单体只会被实例化一次，每个方法和属性都只会创建一次，所以你可以把他们都声明在构造函数内部，例如：

```
var namespace = {};

// 1、最简单的单例
namspace.singeton = {}

// 2、现在我们用一个在定义之后立即执行的函数创造单体
namespace.singleton = function() {
  return {}
}();

```

上述的1、2两个例子中创建的namespace.singeton 完全相同，但是要注意的是第二个例子的匿名函数加了一个括号，这代表着，立即执行返回一个对象给namespace.singleton

有些程序员喜欢在那个匿名函数中在套上一对圆括号，以表示会在声明之后立即执行。这在创建单体较为庞大的时候尤其重要，因为你只要一眼就能看出该函数是用来创建一个闭包。格外加上圆括号，就变成下面这个样子：
```
namespace.singleton = (function() {
  return {}
})();

// 你可以把公用成员添加到单体返回的对象里面
namespace.singleton = (function() {
  // 私有成员
  var _priviteName = "dfdfasfd";
  var _priviteMethod = function() {
    return _priviteName;
  }

  // 公用成员
  return {
    publiceAttribute:true,
    publiceAttribute2:1,
    publiceMenthod:function() {
      ...
    }
  }

  })()
```

** 包装函数创建了一个用来正真添加私有成员的闭包，防止程序员调用到私有成员**
任何声明在这个匿名函数中（但不是那个字面量中）的变量或者函数都只能被在同一个闭包中声明的其他函数访问。这个闭包在匿名函数执行后依然存在，所以在其中声明的函数和变量总能从匿名函数所返回的对象内部（并且只能从内部）访问

相比前者，后者不必再用this.或者namespace.singleton 去访问对象中发成员了

## 惰性单例

前面所讲的单体模式都有一个共同特点：单体对象都是在脚本加载完成之后创建出来的。对于资源密集型或者配置开销很大的单体，也许更加合理的方式是将实例化推迟到需要的时候，这种技术被称为惰性加载，它通常用于那些比较大量数据的单体。

我们如何将普通的闭包单体修改为惰性单体呢？


```
var namespace = {};
namespace.singleton = (function() {
// 第一步，将单体的所有代码移动到一个名为constructor的方法中
function Constructor() {
   var _priviteName = "dfdfasfd";
    var _priviteMethod = function() {
      return _priviteName;
    }
}
 // 公用成员
  return {
    publiceAttribute:true,
    publiceAttribute2:1,
    publiceMenthod:function() {
      ...
    }
  }
})();

```

这个方法不能从外部访问，这是一件好事，因为我们可以完全控制其调用时机。公用方法getInstance就是来实现这种控制的。为了使其成为公用方法，只需将其放到一个对象字面量中并返回该对象即可：

```
var namespace = {};
namespace.singleton = (function() {
// 第一步，将单体的所有代码移动到一个名为constructor的方法中
function Constructor() {
   var _priviteName = "dfdfasfd";
    var _priviteMethod = function() {
      return _priviteName;
    }
}
 // 公用成员
  return {
    // 第二步编写getInstance方法
    getInstance: function() {
      ...
    }
  }
})();

```

现在开始编写控制单体类实例化时机的代码。它需要做两件事情。第一，它必须知道该类是否已经被示例化过。第二，如果该类已经实例化，那么它需要掌握其实例的情况，以便能返回这个实例。

```
var namespace = {};
namespace.singleton = (function() {
 var instance; 
// 第一步，将单体的所有代码移动到一个名为constructor的方法中
function Constructor() {
   var _priviteName = "dfdfasfd";
    var _priviteMethod = function() {
      return _priviteName;
    }

    return {
      getName:function() {
        return "23123"
      },
      publiceMethod2:function() {
        return _priviteMethod()
      }
    }
}
 // 公用成员
  return {
    // 第二步编写getInstance方法
    getInstance: function() {
      if(!instance) {
        instance = Constructor();
      }
      return instance;
    }
  }
})();

```


