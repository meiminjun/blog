title: javascript深入浅出系列-call、apply的使用
date: 2016-03-18 16:10:00
tags:
    - javascript
---

# javascript 继承

``` bash
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>test</title>
  <script>
    function Person(name,age) {
      this.name = name;
      this.age = age;
    }

    Person.prototype.hi = function() {
      document.write("<br/>");
      document.write("大家好,我的名字叫做"+this.name+",我的今年"+this.age);
    };
    Person.prototype.INTEREST = "游泳和打球";
    Person.prototype.MYLOVE = "英雄联盟";
    Person.prototype.toDo = function() {
      document.write("<br/>");
      document.write("我平时的爱好是"+this.INTEREST+"和打"+MYLOVE);
    };
    console.log("----------基类打印---------");
    console.log(Person);
    console.log(Person.__proto__);
    console.log(Person.prototype);
    function Student(name,age,workplace) {
      Person.call(this,name,age);
      this.workplace = workplace;
    }
    console.log("----------子类打印---------");
    console.log(Student);
    console.log(Student.prototype);
    console.log("----------准备继承中---------");
    Student.prototype = Object.create(Person.prototype);
    console.log(Student);
    console.log(Student.prototype);
    Student.prototype.constructor = Student;
    console.log("----------继承之后---------");
    console.log(Student);
    console.log(Student.prototype);
    Student.prototype.hi = function() {
      document.write("<br/>");
      document.write("Hi,我的名字叫做"+this.name+",我的今年"+this.age);
    };

    Student.prototype.learning = function(subject) {
      document.write("<br/>");
      document.write("我很喜欢在"+subject+"在"+this.workplace+"玩"+this.MYLOVE);
    };
    console.log("----------添加prototype属性方法---------");
    console.log(Student);
    console.log(Student.prototype);

    console.log("----------对象实例化开始---------");
    var jason = new Student("Jason","18","家");
    console.log(jason);
    console.log(jason.hi());
    console.log(jason.INTEREST);
    console.log(jason.learning("周末的时候"));
  </script>
</head>
<body>

</body>
</html>

```
