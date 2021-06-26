# JavaScript

## 简介

JS是弱类型，Java 是强类型。(换句话说，JS定义的变量是可以改变类型的，Java中(int、double)类型就确定了)

特点： 

1. 交互性（它可以做的就是信息的动态交互） 
2. 安全性（不允许直接访问本地硬盘） 
3. 跨平台性（只要是可以解释 JS 的浏览器都可以执行，和平台无关）

## JavaScript和html代码的结合方式

### **第一种方式** 

在 **head** 标签中，或者在 **body** 标签中， 使用 **script 标签** 来书写 JavaScript 代码

```
<script type="text/javascript">
alert("hello javaScript!");
</script>
```
alert 是 JavaScript 语言提供的一个警告框函数

它可以接收任意类型的参数，这个参数就是警告框的提示信息

当然，如果先后有两个alert，那网页会先后分两次弹出alert的内容

### 第二种方式

使用 script 标签引入 单独的 JavaScript 代码文件

```
    <script type="text/javascript" src="01.js"></script>
    <script type="text/javascript"></script>
```



## 变量 

**可以存放某些值的内存的命名。** 

JavaScript 的变量类型： 

+ 数值类型	 			number 
+ 字符串类型	 		string
+ 对象类型				object
+ 布尔类型				boolean 
+ 函数类型                function 

JavaScript 里特殊的值： 

undefined                               未定义，所有 js 变量未赋于初始值的时候，默认值都是 undefined. 

null                                          空值 

NaN                                         Not a Number。非数字。非数值。 

JS 中的定义变量格式： 

```var 变量名; ```

```var 变量名 = 值;```

> 意外发现：
>
> 当定义了一个number类型的a=12；
>
> 又定义了一个string类型的b=abc;
>
> alert(typeof b * a);的类型为NAN
> 
> alert(typeof (b * a);的类型却是number
>
> 排除了a，b的先后原因，更具体原因未知

## 关系运算符

等于：                ==                         等于是简单的做字面值的比较 

全等于：            ===                       除了做字面值的比较之外，还会比较两个变量的数据类型

## **逻辑运算** 

且运算：            && 

或运算：           || 

取反运算：        !

> 在 JavaScript 语言中，所有的变量，都可以做为一个 boolean 类型的变量去使用。 
>
> **0 、null、 undefined、””(空串) 都认为是 false；**
>
> ps：空串为假但是，空串不等于空格，空格为真

&& 运算。  

第一种：当表达式全为真的时候。返回最后一个表达式的值。 

第二种：当表达式中，有一个为假的时候。返回第一个为假的表达式的值



|| 运算 

第一种情况：当表达式全为假时，返回最后一个表达式的值 

第二种情况：只要有一个表达式为真。就会把回第一个为真的表达式的值



## 数组

JS中数组的定义： 

格式： 

var 数组名 = [];

> 空数组 

var 数组名 = [1 , ’abc’ , true]; 

> 定义数组同时赋值元素 

```
<script type="text/javascript">
        var arr = [];
        arr[0] = 1;
        arr[1] = "asd";
        arr[2] = "xy";
        for(var i = 0;i < arr.length;i++){
            alert(arr[i]);
        }
</script>
```

## 函数

+ function 函数名(形参列表){ 

  ​    函数体 

  }

> return 语句可以返回值！

```
<script type="text/javascript">
    function sum(num1,num2){
        var result = num1 + num2;
        alert(num1);
        alert(num2);
        return result;
    }
    alert(sum(100,50));
</script>
```

+ var 函数名 = function(形参列表){ 

  ​    函数体 

  }


> JS 中函数的重载会直接覆盖掉上一次的定义

```
     function fun(){
         alert("无参函数 fun()");
     }
     function fun(a,b){
         alert("有参函数 fun(a,b)");
     }
     fun();
     //显然结果是后面那个
```

+ **arguments** **隐形参数**

  是在 function 函数中不需要定义，但却可以直接用来获取所有参数的变量

  ```
          function fun(a){
              alert( arguments.length );//1
              alert( arguments[0] );    //2
              alert( arguments[1] );    //3
              alert( arguments[2] );    //4
              alert("a = " + a);        //5
              for (var i = 0; i < arguments.length; i++){
                  alert( arguments[i] );
              }
              alert("无参函数 fun()");
          }
          fun(1,"ad");
          //运行后的结果为2(对应1)、1(对应2)、ad(对应3)、undefined(对应4，因为未定义)、
          //a = 1(对应5)最后1、ad、无参函数 fun()(对应循环和alert)
  ```

  

## 自定义对象

+ **Object** **形式的自定义对象**

  对象的定义： 

  ​    var 变量名 = new Object();     // 对象实例（空对象） 

  > 这里一定要大写O！！

  ​    变量名.属性名 = 值;                  // 定义一个属性 

  ​    变量名.函数名 = function(){}    // 定义一个函数 

  对象的访问： 
  
  ​    变量名.属性/函数名();
  
  ```
  <script type="text/javascript">
      var obj = new Object();
      obj.name = "华仔";
      obj.age = 18;
      obj.fun = function (){
          alert("姓名：" + this.name + " , 年龄：" + this.age);
          }
      alert( obj.age );
      obj.fun();
  </script>
  ```
  
+ **{}花括号形式的自定义对象** 

  对象的定义： 

  ​    var 变量名 = { 

  ​        属性名：值,                     // 定义一个属性 

  ​        属性名：值,                     // 定义一个属性 

  ​        函数名：function(){}      //定义一个函数 

  }; 

  对象的访问： 

  ​    变量名.属性 / 函数名();

  ```
      var obj = {
          name:"QAQ",
          age:18,
          fun : function(){
              alert("姓名：" + this.name + " , 年龄：" + this.age);
          }
      };
      alert(obj.name);
      obj.fun();
  ```

  

## 事件

事件就是电脑输入设备与页面进行**交互**的响应

+ **常用的事件：**

  | 事件                      | 作用                                             |
  | ------------------------- | ------------------------------------------------ |
  | onload 加载完成事件       | 页面加载完成之后，常用于做页面 js 代码初始化操作 |
  | onclick 单击事件          | 常用于按钮的点击响应操作                         |
  | onblur 失去焦点事件       | 常用用于输入框失去焦点后验证其输入内容是否合法   |
  | onchange 内容发生改变事件 | 常用于下拉列表和输入框内容发生改变后操作         |
  | onsubmit 表单提交事件     | 常用于表单提交前，验证所有表单项是否合法         |

+ **静态注册和动态注册**

  > 事件的注册就是告诉浏览器，当事件响应后要执行哪些操作代码，叫事件注册或事件绑定。

  **静态**注册事件：通过 html 标签的事件属性直接赋于事件响应后的代码，这种方式我们叫静态注册。

  **动态**注册事件：是指先通过 js 代码得到标签的 dom 对象，然后再通过 dom 对象.事件名 = function(){} 这种形式赋于事件响应后的代码，叫动态注册。

  动态注册基本步骤： 

  + 获取标签对象 

  + 标签对象.事件名 = fucntion(){}

  

