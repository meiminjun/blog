title: javascript深入浅出系列-Array 之 splice
date: 2016-06-23 21:57:13
tags:
  - javascript
---

# javascript 中的splice 方法介绍和示例

## 定义和用法

javascript 中的 splice 方法很强大, splice() 方法用于插入、删除或替换数组的元素。

## 语法

> arrayObject.splice(index,howmany,element1,.....,elementX)

| 参数        | 描述   |
| --------   | -----:  |
| index     | 必需。规定从何处添加/删除元素。该参数是开始插入和（或）删除的数组元素的下标，必须是数字。 |
| howmany        |   必需。规定应该删除多少元素。必须是数字，但可以是 "0"。如果未规定此参数，则删除从 index 开始到原数组结尾的所有元素。   |
| element1        |    可选。规定要添加到数组的新元素。从 index 所指的下标处开始插入。    |
| elementX        |    可选。可向数组添加若干元素。   |

## 返回值

如果从 arrayObject 中删除了元素，则返回的是含有**被删除**的元素的数组。

> 注释：请注意，splice() 方法与 slice() 方法的作用是不同的，**splice() 方法会直接对数组进行修改。影响原有数组** 

## 说明

* 删除：用于删除元素，两个参数，第一个参数（要删除第一项的位置），第二个参数（要删除的项数）
* 插入：向数组指定位置插入任意项元素。三个参数，第一个参数（起始位置），第二个参数（0），第三个参数（插入的项）
* 替换：向数组指定位置插入任意项元素，同时删除任意数量的项，三个参数。第一个参数（起始位置），第二个参数（删除的项数），第三个参数（插入任意数量的项）

``` bash
var lang = ["php","java","javascript"];
//删除
var removed = lang.splice(1,1);
alert(lang); //php,javascript
alert(removed); //java ,返回删除的项
//插入(第二个元素为0的时候)
var insert = lang.splice(0,0,"asp"); //从第0个位置开始插入
alert(insert); //返回空数组
alert(lang); //asp,php,javascript
//替换
var replace = lang.splice(1,1,"c#","ruby"); //删除一项，插入两项
alert(lang); //asp,c#,ruby
alert(replace); //php,返回删除的项
```

> 说明: splice 第二个参数为 0 代表插入 或者 大于0 的为删除
