title: javascript深入浅出系列-Function 之 call、apply
date: 2016-03-18 16:10:00
tags:
  - javascript
---

## call与apply的区别
---

call 与 apply 的用法是基本一致,只是调用是不一样:
call的第二个参数为"字符串"
apply 的第二个参数为"数组"

## 方法调用
---

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>test</title>
  <script>
    function Animal(){
        this.name = "Animal";
        this.showName = function(){
            alert(this.name);
        }
    }

    function Cat(){
        this.name = "Cat";
    }

    var animal = new Animal();
    var cat = new Cat();

    //通过call或apply方法，将原本属于Animal对象的showName()方法交给对象cat来使用了。
    //输入结果为"Cat"
    animal.showName.call(cat,"");
    //animal.showName.apply(cat,[]);
  </script>
</head>
<body>

</body>
</html>

```
> call 的意思是把 animal 的方法放到cat上执行，原来cat是没有showName() 方法，现在是把animal 的showName()方法放到 cat上来执行，所以this.name 应该是 Cat

## 实现继承

---

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>test</title>
  <script>
    function Person(name){
        this.name = name;
        this.showName = function(){
            alert(this.name);
        }
    }

    function Student(name){
        // 简单继承
        Person.call(this, name);
    }

    var student = new Student("学生");
    student.showName();
  </script>
</head>
<body>

</body>
</html>

```

>  Person.call(this) 的意思就是使用 Person对象代替this对象，那么 Student中不就有Person的所有属性和方法了吗，Student对象就能够直接调用Person的方法以及属性了.
