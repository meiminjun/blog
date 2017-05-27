title: javascript深入浅出系列-常用DOM操作
date: 2016-01-05 15:57:13
tags:
	- javascript
---

这里主要讲一下开发中经常用到的一些javascript原生操作dom的方法

<!-- more -->

## document.getElementById()  

根据Id获取元素节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      function fun1() {
          var str = document.getElementById("p1").innerHTML;
          alert(str);        //弹出    我是第一个P
      }
    </script>
</head>
<body>
    <div id="div1">
         <p id="p1">我是第一个P</p>
         <p id="p2">我是第二个P</p>
     </div>
</body>
</html>

```

##  document.getElementsByName()   

 根据name获取元素节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      function fun1() {
          var username = document.getElementsByName("userName")[0].value;
          alert(username);    //输出userName里输入的值
      }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1">
            我是第一个P</p>
        <p id="p2">
            我是第二个P</p>
        <input type="text" value="请输入值" name="userName" />
        <input type="button" value="确定" onclick="fun1()">
    </div>
</body>
</html>

```


##  document.getElementsByTagName()  

根据HTML标签名获取元素节点，注意getElements***的选择器返回的是一个NodeList对象，能根据索引号选择其中1个，可以遍历输出。

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      window.onload = function () {
        var str = document.getElementsByTagName("p")[1].innerHTML;
        alert(str);        //输出  我是第二个P，因为获取的是索引为1的P，索引从0开始

        var arr = document.getElementsByTagName("p");
        for (var i = 0; i < arr.length; i++) {
            alert(arr[i].innerHTML);
        }

        var node = document.getElementById("div1");
        var node1 = document.getElementsByTagName("p")[1];    //从获取到的元素再获取
           alert(node1.innerHTML);
      }
    </script>
</head>
<body>
    <div id="div1">
       <p id="p1">
           我是第一个P</p>
       <p id="p2">
           我是第二个P</p>
    </div>
</body>
</html> 

```

##  document.getElementsByClassName()    

根据class获取元素节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      window.onload = function () {
        var node = document.getElementsByClassName("class1")[0];
        alert(node.innerHTML);
      }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1" class="class1">
                我是第一个P</p>
        <p id="p2" class="class2">
                我是第二个P</p>
    </div>
</body>
</html>

```

## javascript中的CSS选择器
``` html
    document.querySelector()    //根据CSS选择器的规则，返回第一个匹配到的元素
    document.querySelectorAll()    //根据CSS选择器的规则，返回所有匹配到的元素

    <html>
    <head>
        <title></title>
        <script type="text/javascript">
          window.onload = function () {
            var node = document.querySelector("#div1 > p");
            alert(node.innerHTML);                //输出  我是第一个P

            var node1 = document.querySelector(".class2");
            alert(node1.innerHTML);                //输出  我是第二个P

            var nodelist = document.querySelectorAll("p");
            alert(nodelist[0].innerHTML + " - " + nodelist[1].innerHTML);    //输出  我是第一个P - 我是第二个P
          }
        </script>
    </head>
    <body>
        <div id="div1">
            <p id="p1" class="class1">
                    我是第一个P</p>
            <p id="p2" class="class2">
                    我是第二个P</p>
        </div>
    </body>
    </html>

```

##  文档结构和遍历

* 作为节点数的文档

1. parentNode    获取该节点的父节点
2. childNodes    获取该节点的子节点数组
3. firstChild    获取该节点的第一个子节点
4. lastChild    获取该节点的最后一个子节点
5. nextSibling    获取该节点的下一个兄弟元素
6. previoursSibling    获取该节点的上一个兄弟元素
7. nodeType    节点的类型，9代表Document节点，1代表Element节点，3代表Text节点，8代表Comment节点，11代表DocumentFragment节点
8. nodeVlue    Text节点或Comment节点的文本内容
9. nodeName    元素的标签名(如P,SPAN,#text(文本节点),DIV)，以大写形式表示

> **注意，以上6个方法连元素节点也算一个节点**

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      window.onload = function () {
         var node1 = document.querySelector(".class2");
         alert(node1.parentNode.innerHTML); //输出  <p id="p1" class="class1">我是第一个P</p><p id="p2" class="class2">我是第二个P</p>

         var nodelist = document.getElementById("div1");
         var arr = nodelist.childNodes;
         alert(arr[1].innerHTML + " - " + arr[3].innerHTML); //输出    我是第一个P - 我是第二个P 为什么是1，3呢？因为本方法文本节点也会获取，也就是说0,2,4是文本节点

         var node = document.getElementById("div2");
         for (var i = 0; i < node.childNodes.length; i++) {
             if (node.childNodes[i].nodeType == 1) {
                 alert(node.childNodes[i].innerHTML);
             }
             else if (node.childNodes[i].nodeType == 3) {
                 alert(node.childNodes[i].nodeValue);
             }
         }
      }

    </script>
</head>
<body>
    <div id="div1">
        <p id="p1" class="class1">
                我是第一个P</p>
        <p id="p2" class="class2">
                我是第二个P</p>
    </div>

    <div id="div2">
          文本1
          <p id="p1" class="class1">
              我是第一个P</p>
          文本2
          <p id="p2" class="class2">
              我是第二个P</p>
          文本3
    </div>
</body>
</html>

```

* 作为元素树的文档    

1. firstElementChild        第一个子元素节点
2. lastElementChild        最后一个子元素节点
3. nextElementSibling        下一个兄弟元素节点
4. previousElementSibling    前一个兄弟元素节点
5. childElementCount        子元素节点个数量


> **注意，此5个方法文本节点不算进去**

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      window.onload = function () {
         var node = document.getElementById("div1");
         var node1 = node.firstElementChild;
         var node2 = node.lastElementChild;

         alert(node.childElementCount);  //输出2，div1一共有两个非文档子元素节点
         alert(node1.innerHTML);         //输出 我是第一个P
         alert(node2.innerHTML);         //输出 我是第二个P
         alert(node2.previousElementSibling.innerHTML);  //输出 我是第一个P(第二个元素节点的上一个非文本元素节点是P1)
         alert(node1.nextElementSibling.innerHTML);      //输出 我是第二个P(第一个元素节点的下一个兄弟非文本节点是P2)
      }
    </script>
</head>
<body>
    <div id="div1">
      <p id="p1" class="class1">
          我是第一个P</p>
      <p id="p2" class="class2">
          我是第二个P</p>
    </div>
</body>
</html>

```

## javascript操作HTML属性

属性的读取，此处要注意的是，某些HTML属性名称在javascript之中是保留字，因此会有些许不同，如class,lable中的for在javascript中变为htmlFor,className

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      window.onload = function () {
          var nodeText = document.getElementById("input1");
          alert(nodeText.value);        //输出 我是一个文本框
          var nodeImg = document.getElementById("img1");
          alert(nodeImg.alt);            //输出 我是一张图片
          var nodeP = document.getElementById("p1");
          alert(nodeP.className);        //输出 class1    注意获取class是className，如果写成nodeP.class则输出undefined
      }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1" class="class1"> 我是第一个P</p>
        <img src="123.jpg" alt="我是一张图片" id="img1" />
        <input type="text" value="我是一个文本框" id="input1" />
    </div>
</body>
</html>

```

### 属性的设置，此处同样要注意的是保留字

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
      function fun1() {
          document.getElementById("img1").src = "1small.jpg";        //改变图片的路径属性。实现的效果为，当点击图片时，大图变小图。
      }
    </script>
</head>
<body>
    <div id="div1">
        <img src="1big.jpg" alt="我是一张图片" class="imgClass" id="img1" onclick="fun1()" />
    </div>
</body>
</html>

```

### 非标准HTML属性

getAttribute()    // 注意这两个方法是不必理会javascript保留字的，HTML属性是什么就怎么写。
setAttribute();

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        function fun1() {
            document.getElementById("img1").setAttribute("src", "1small.jpg");
            alert(document.getElementById("img1").getAttribute("class"));
        }
    </script>
</head>
<body>
    <div id="div1">
        <img src="1big.jpg" alt="我是一张图片" class="imgClass" id="img1" onclick="fun1()" />
    </div>
</body>
</html>

```


### Attr节点的属性

attributes属性  非Element对象返回null，Element一半返回Attr对象。Attr对象是一个特殊的Node,通过name与value获取属性名称与值。
如:document.getElementById("img1")[0];
   document.getElementById("img1").src;

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        function fun1() {
            alert(document.getElementById("img1").attributes[0].name);    //输出  onclick    注意，通过索引器访问是写在右面在排前面，从0开始
            alert(document.getElementById("img1").attributes.src.value);    //输出1big.jpg
            document.getElementById("img1").attributes.src.value = "1small.jpg";    //点击后改变src属性，实现了点击大图变小图效果
        }
    </script>
</head>
<body>
    <div id="div1">
        <img src="1big.jpg" alt="我是一张图片" class="imgClass" id="img1" onclick="fun1()" />
    </div>
</body>
</html>

```

## 元素的内容

### innerText、textContent
innerText与textContent的区别，当文本为空时，innerText是""，而textContent是undefined
### innerHTML

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
          alert(document.getElementById("p1").innerText);  //注意火狐浏览器不支持innerText
          alert(document.getElementById("p1").textContent);    //基本都支持textContent
          document.getElementById("p1").textContent = "我是p1，javascript改变了我";    //设置文档Text
          alert(document.getElementById("p2").textContent);
          alert(document.getElementById("p2").innerHTML); //innerHTML与innerText的区别，就是对HTML代码的输出方式Text不会输出HTML代码
        }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1">我是第一个P</p>
        <p id="p2">我是第<b>二</b>个P</p>
    </div>
</body>
</html>

```

## 创建，插入，删除节点

### document.createTextNode()    

创建一个文本节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
          var textNode = document.createTextNode("<p>我是一个javascript新建的节点</p>");
          document.getElementById("div1").appendChild(textNode);
        }
    </script>
</head>
<body>
    <div id="div1">
      <p id="p1">我是第一个P</p>
      <p id="p2">我是第二个P</p>
    </div>
</body>
</html>

  <!-- 执行完成后HTML代码变为：
  <div id="div1">
      <p id="p1">我是第一个P</p>
      <p id="p2">我是第二个P</p>
      我是一个javascript新建的节点
  </div>
  -->

```

### document.createElement()  

创建一个元素节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
          var pNode = document.createElement("p");
          pNode.textContent = "新建一个P节点";
          document.getElementById("div1").appendChild(pNode);
        }
    </script>
</head>
<body>
    <div id="div1">
      <p id="p1">我是第一个P</p>
      <p id="p2">我是第二个P</p>
    </div>
</body>
</html>

  <!-- 执行完成后HTML代码变为：
  <div id="div1">
      <p id="p1">我是第一个P</p>
      <p id="p2">我是第二个P</p>
      <p>新建一个P节点</p>
  </div>
  -->

```

### 插入节点

 appendChild()    //将一个节点插入到调用节点的最后面
 insertBefore()    //接受两个参数，第一个为待插入的节点，第二个指明在哪个节点前面，如果不传入第二个参数，则跟appendChild一样，放在最后。

 ``` html
 <html>
 <head>
     <title></title>
     <script type="text/javascript">
         window.onload = function () {
             var pNode1 = document.createElement("p");
             pNode1.textContent = "insertBefore插入的节点";
             var pNode2 = document.createElement("p");
             pNode2.textContent = "appendChild插入的节点";
             document.getElementById("div1").appendChild(pNode2);
             document.getElementById("div1").insertBefore(pNode1,document.getElementById("p1"));
         }
     </script>
 </head>
 <body>
     <div id="div1">
        <p id="p1">我是第一个P</p>
      </div>
 </body>
 </html>

   <!-- 执行完成后HTML代码变为：
   <div id="div1">
        <p>insertBefore插入的节点</p>
        <p id="p1">我是第一个P</p>
        <p>appendChild插入的节点</p>
    </div>
   -->
 ```

## 删除和替换节点

### removeChild()

由父元素调用，删除一个子节点。注意是直接父元素调用，删除直接子元素才有效，删除孙子元素就没有效果了

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
            var div1 = document.getElementById("div1");
            div1.removeChild(document.getElementById("p2"));
        }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1">我是第一个P</p>
        <p id="p2">我是第二个P</p>
    </div>
</body>
</html>


  <!-- 执行完成后HTML代码变为：
  <div id="div1">
      <p id="p1">我是第一个P</p>    //注意到第二个P元素已经被移除了
  </div>
  -->

```

### replaceChild()   

删除一个子节点，并用一个新节点代替它，第一个参数为新建的节点，第二个节点为被替换的节点

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
            var div1 = document.getElementById("div1");
            var span1 = document.createElement("span");
            span1.textContent = "我是一个新建的span";
            div1.replaceChild(span1,document.getElementById("p2"));
        }
    </script>
</head>
<body>
    <div id="div1">
        <p id="p1">我是第一个P</p>
        <p id="p2">我是第二个P</p>
    </div>
</body>
</html>

  <!-- 执行完成后HTML代码变为：
  <div id="div1">
      <p id="p1">我是第一个P</p>
      <span>我是一个新建的span</span>    //留意到p2节点已经被替换为span1节点了
  </div>
  -->
```

## javascript操作元素CSS

通过元素的style属性可以随意读取和设置元素的CSS样式，例子：

``` html
<html>
<head>
    <title></title>
    <script type="text/javascript">
        window.onload = function () {
            alert(document.getElementById("div1").style.backgroundColor);
            document.getElementById("div1").style.backgroundColor = "yellow";
        }
    </script>
</head>
<body>
    <div id="div1" style="width:100px; height:100px; background-color:red"></div>
</body>
</html>
```














