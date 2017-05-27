title: javascript深入浅出系列-Function 之 静态属性和原型方法
date: 2016-06-23 21:57:13
tags:
  - javascript
---

# 静态属性和原型方法

``` bash
    // 对象构造函数  
    function Atest(name){  
      //私有属性，只能在对象构造函数内部使用  
      var className = "Atest";  
      //公有属性,在对象实例化后调用  
      this.name = name;  
      //对象方法  
      this.hello = function(){  
        alert(this.name);  
        alert(this.msg());//使用原型方法扩充的方法可以在类内部使用  
        alert(this.sex);//使用原型方法扩充的属性可以在类内部使用  
        alert(Atest.age);//静态属性调用时格式为[对象.静态属性]  
      }  
    }  
    //类方法 (实际是静态方法直接调用) 位置：Person类的外部 语法格式：类名称.方法名称 = function([参数...]){ 语句行; }  
    Atest.Run = function(){  
      alert("我是类方法 Run");  
    }  

    //原型方法  
    Atest.prototype.msg = function(){  
      alert("我的名字是："+this.name);//如果原型方法当作静态方法直接调用时，this.name无法被调用  
    }  

    //公有静态属性 在类的外部  
    Atest.age = 20;//公有静态属性不能使用 【this.属性】，只能使用 【对象.属性】 调用  

    //原型属性，当作是类内部的属性使用【this.原型属性】，也可以当成公有静态属性使用【对象.prototype.原型属性】  
    Atest.prototype.sex = "男";  

    Atest.Run(); //类方法也是静态方法，可以直接使用 【对象.静态方法()】  
    Atest.prototype.msg();//原型方法当成静态方法使用时【对象.prototype.方法()】   
    alert(Atest.prototype.sex);//原型属性当作静态属性使用时【对象.prototype.方法()】  
    var a = new Atest("zhangsan");//对象方法和原型方法需要实例化对象后才可以使用  
    a.hello();//对象方法必须实例化对象  
    a.msg();//原型方法必须实例化对象  
    alert(a.age);//错误，公有静态属性只能使用 【对象.属性】调用  

    //ps:尽量将方法定义为原型方法，原型方法避免了每次调用构造函数时对属性或方法的构造，节省空间,创建对象快.  

```