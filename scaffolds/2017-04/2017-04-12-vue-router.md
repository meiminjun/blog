title: vue-router 三种加载方式速度评测
date: 2017-04-12 22:57:13
tags:
  - vue
  - vue-router
  - webpack
---

![](https://ww4.sinaimg.cn/large/006tNc79gy1feuj2phraug30gn0c1qv7.gif)

## [ensure 方式](https://github.com/vuejs/vue-router/blob/next/examples/lazy-loading/app.js)

```
// const Index = r => require.ensure([], () => r(require('@/views/deposit/deposit_index')), 'Index')
// const Product = r => require.ensure([], () => r(require('@/views/deposit/deposit_product')), 'Product')
// const ProductSave = r => require.ensure([], () => r(require('@/views/deposit/deposit_product_save')), 'ProductSave')
// const My = r => require.ensure([], () => r(require('@/views/deposit/deposit_my')), 'My')
// const MyDetail = r => require.ensure([], () => r(require('@/views/deposit/deposit_my_detail')), 'MyDetail')
// const MyTransDetail = r => require.ensure([], () => r(require('@/views/deposit/deposit_my_transdetail')), 'MyTransDetail')
```

全部采用ensure的方式运行,首屏时间则会慢很多，每次打开的时间记录
```
首屏时间: 324ms
首屏时间: 552ms
首屏时间: 457ms
首屏时间: 275ms
首屏时间: 250ms
首屏时间: 330ms
首屏时间: 395ms
首屏时间: 314ms
首屏时间: 276ms
首屏时间: 314ms

```

**平均时间：348.7ms**

下面测试跳转时的时间如下：
```
首页跳转测试: 212ms
首页跳转测试: 161ms
首页跳转测试: 161ms
首页跳转测试: 54.8ms
首页跳转测试: 156ms
首页跳转测试: 58.3ms
首页跳转测试: 52.3ms
首页跳转测试: 84.2ms
首页跳转测试: 150ms
首页跳转测试: 168ms

```

**平均时间：125.76ms**


## amd 方式

```
const Index = resolve => require(['@/views/deposit/deposit_index'], resolve)
const Product = resolve => require(['@/views/deposit/deposit_product'], resolve)
const ProductSave = resolve => require(['@/views/deposit/deposit_product_save'], resolve)
const My = resolve => require(['@/views/deposit/deposit_my'], resolve)
const MyDetail = resolve => require(['@/views/deposit/deposit_my_detail'], resolve)
const MyTransDetail = resolve => require(['@/views/deposit/deposit_my_transdetail'], resolve)
```

如果是webpack2 可以使用
```
// const Index = () => System.import('@/views/deposit/deposit_index')

```

首屏时间如下：

```
首屏时间: 480ms
首屏时间: 425ms
首屏时间: 310ms
首屏时间: 360ms
首屏时间: 318ms
首屏时间: 328ms
首屏时间: 502ms
首屏时间: 324ms
首屏时间: 313ms
首屏时间: 505ms
```

**平均时间：386.5ms**

下面测试按照amd方式跳转时的时间如下：
```
首页跳转测试: 50.6ms
首页跳转测试: 48.2ms
首页跳转测试: 51.2ms
首页跳转测试: 54.0ms
首页跳转测试: 48.5ms
首页跳转测试: 49.1ms
首页跳转测试: 48.4ms
首页跳转测试: 41.9ms
首页跳转测试: 46.2ms
首页跳转测试: 47.4ms
```

平均时间：48.55ms

## 常规加载方式

```
import Index from '@/views/deposit/deposit_index'
import Product from '@/views/deposit/deposit_product'
import ProductSave from '@/views/deposit/deposit_product_save'
import My from '@/views/deposit/deposit_my'
import MyDetail from '@/views/deposit/deposit_my_detail'
import MyTransDetail from '@/views/deposit/deposit_my_transdetail'
```

全部采用这种方式，速度会要快很多，首屏时间如下
```
首屏时间: 111ms
首屏时间: 119ms
首屏时间: 76.6ms
首屏时间: 76.5ms
首屏时间: 72.8ms
首屏时间: 108ms
首屏时间: 122ms
首屏时间: 84.3ms
首屏时间: 123ms
首屏时间: 113ms
```

**平均时间：100.62ms**

采用此方式做跳转测试，如下
```
首页跳转测试: 26.9ms
首页跳转测试: 25.0ms
首页跳转测试: 31.2ms
首页跳转测试: 31.1ms
首页跳转测试: 23.7ms
首页跳转测试: 26.6ms
首页跳转测试: 29.4ms
首页跳转测试: 27.6ms
首页跳转测试: 30.2ms
首页跳转测试: 24.2ms
```

**平均时间为：27.59ms**

总结：


加载方式 | 首屏平均时间 | 跳转页面平均时间
---      | ---  | ---
常规加载 | 100.62ms|27.59ms
amd加载  | 386.5ms |48.55ms
ensure加载   | 348.7ms |125.76ms


## amd 与 ensure 区别

* require-amd 
    
说明: 同AMD规范的require函数，使用时传递一个模块数组和回调函数，模块都被下载下来且都被执行后才执行回调函数

语法: require(dependencies: String[], [callback: function(...)])
参数 
dependencies: 模块依赖数组
callback: 回调函数


* require-ensure 

说明: require.ensure在需要的时候才下载依赖的模块，当参数指定的模块都下载下来了（下载下来的模块还没执行），便执行参数指定的回调函数。require.ensure会创建一个chunk，且可以指定该chunk的名称，如果这个chunk名已经存在了，则将本次依赖的模块合并到已经存在的chunk中，最后这个chunk在webpack构建的时候会单独生成一个文件。

语法: require.ensure(dependencies: String[], callback: function([require]), [chunkName: String])
dependencies: 依赖的模块数组
callback: 回调函数，该函数调用时会传一个require参数
chunkName: 模块名，用于构建时生成文件时命名使用

注意点：requi.ensure的模块只会被下载下来，不会被执行，只有在回调函数使用require(模块名)后，这个模块才会被执行。

