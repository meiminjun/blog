title: javascript深入浅出系列-String 之 slice
date: 2016-06-23 21:57:13
tags:
  - javascript
---

# javascript 字符串中的slice 方法介绍和示例

## 定义和用法

slice() 方法可提取字符串的某个部分，并以新的字符串返回被提取的部分。

## 语法

> stringObject.slice(start,end)

| 参数        | 描述   |
| --------   | -----:  |
| start     | 要抽取的片断的起始下标。如果是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推。 |
| end       | 紧接着要抽取的片段的结尾的下标。若未指定此参数，则要提取的子串包括 start 到原字符串结尾的字符串。如果该参数是负数，那么它规定的是从字符串的尾部开始算起的位置。   |

## 返回值

一个新的字符串。包括字符串 stringObject 从 start 开始（包括 start）到 end 结束（**不包括 end**）为止的所有字符。

> 注释：请注意，splice() 方法与 slice() 方法的作用是不同的，**splice() 方法会直接对数组进行修改。影响原有数组** 

## 说明

String 对象的方法 slice()、substring() 和 substr() （不建议使用）都可返回字符串的指定部分。slice() 比 substring() 要灵活一些，因为它允许使用负数作为参数。slice() 与 substr() 有所不同，因为它用两个字符的位置来指定子串，而 substr() 则用字符位置和长度来指定子串。

``` bash
// 提取从位置 6 开始的所有字符
var str="Hello happy world!"
document.write(str.slice(6));  // happy world!

// 提取从位置 6 到位置 11 的所有字符
var str="Hello happy world!"
document.write(str.slice(6,11)) // happy

```

# javascript 数组中的slice 的用法

## 定义和用法

slice() 方法可从已有的数组中返回选定的元素。

## 语法

> arrayObject.slice(start,end)

| 参数        | 描述   |
| --------   | -----:  |
| start     | 必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。 |
| end       | 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。   |

## 返回值

返回一个新的数组，包含从 start 到 end （不包括该元素）的 arrayObject 中的元素。

## 说明

请注意，该方法并不会修改数组，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。

提示和注释

注释：您可使用负值从数组的尾部选取元素。

注释：如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。

## 示例

### 传递一个参数
```
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

document.write(arr + "<br />") // George,John,Thomas
document.write(arr.slice(1) + "<br />") // John,Thomas
document.write(arr)   // George,John,Thomas

```

### 传递两个参数

``` bash
var arr = new Array(6)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
arr[3] = "James"
arr[4] = "Adrew"
arr[5] = "Martin"

document.write(arr + "<br />")  
// George,John,Thomas,James,Adrew,Martin

document.write(arr.slice(2,4) + "<br />")
// Thomas,James

document.write(arr)
// George,John,Thomas,James,Adrew,Martin

```