## CSS

1. CSS 是「层叠样式表单」。是用于(增强)控制网页样式并允许将样式信息与网页内容分离的一种标记性语言。

2. CSS的格式一般为：

   ```
   选择器{
       属性: 值;
   }
   例如：
   p{
       color:red;
       font-size:30px;
   }
   ```
  
3. CSS 注释：/*注释内容*/

## **CSS** **和** **HTML** **的结合方式** 

+ 在标签的 style 属性上设置”key:value value;”，修改标签样式。

  ```
  <div style="border: 1px solid red;">div标签</div>
  <span style="border: 1px solid red;">span标签</span>
  ```

  >样式多了。代码量非常庞大。 
  >
  >可读性非常差。 
  >
  >Css 代码没什么复用性可方言。

+ 在 head 标签中，使用 style 标签来定义各种自己需要的 css 样式。 

  ```
  xxx {
    Key : value value; 
  }
div{
      border: 1px solid red;
  }
  ```

  > 只能在同一页面内复用代码，不能在多个页面中复用 css 代码。 
  >
  > 维护起来不方便，实际的项目中会有成千上万的页面，要到每个页面中去修改。工作量太大了。

+ 把 css 样式写成一个单独的 css 文件，再通过 link 标签引入即可复用。

  > 使用 html 的 <link rel=*"stylesheet"* type=*"text/css"* href=*"./styles.css" /*> 标签 导入 css 样 
  >
  > 式文件。

  CSS文件内容

  ```
  div{
      border: 1px solid yellow;
  }
  span{
      border: 1px solid red;
  }
  ```

  html 文件内容

  ```
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
      <!--link 标签专门用来引入 css 样式代码-->
      <link rel="stylesheet" type="text/css" href="1.css"/>
      
  </head>
      <body>
      <div>div 标签 1</div>
      <div>div 标签 2</div>
      <span>span 标签 1</span>
      <span>span 标签 2</span>
      </body>
  </html>
  ```

## CSS选择器

+ **标签名选择器** 

  标签名{ 

  ​    属性：值; 

  }

  head部分

  ```
  <style type="text/css">
      <!--这里将style对象的type属性设置为"text/css"，是允许不支持这类型的浏览器忽略样式表单-->
      div{
      	border: 1px solid yellow;
      	color: blue;
      	font-size: 30px;
  	}
  </style>
  ```

  body部分

  ```
  <div>div标签</div>
  ```

+ **id选择器** 

  \#id 属性值{ 

  ​    属性：值; 

  }
  
  ```
  <style type="text/css">
  	#id001{
      	color: blue;
      	font-size: 30px;
      	border: 1px yellow solid;
  	}
  </style>
  ```
  
  ```
  <div id="id001">div标签</div>
  ```
  
+ **class选择器(类选择器)**

  **.**class 属性值{ 

  ​    属性：值; 

  } 

  ```
  <style type="text/css">
  	.class01{
     		color: blue;
      	font-size: 30px;
      	border: 1px solid yellow;
  	}
  </style>
  ```

  ```
  <div class="class01">div标签class01</div>
  ```

+ **组合选择器**

  选择器 1，选择器 2，选择器 n{ 

  ​    属性：值; 

  } 

  ```
  <style type="text/css">
  	.class01 , #id01{
  		color: blue;
  		font-size: 20px;
  		border: 1px yellow solid;
  	}
  </style>
  ```

  ```
  <div id="id01">div标签id01</div>
  <div class="class01">div标签class01</div>
  ```

  

## 常用样式

1. 字体颜色   ```color：red；``` 

   颜色可以写颜色名如：black, blue, red, green 等 

   颜色也可以写 rgb值和十六进制表示值：如 rgb(255,0,0)，#00F6DE，如果写十六进制值必须加#

2. 宽度  ```width:19px; ```
   
   宽度可以写像素值：19px； 
   
   也可以写百分比值：20%；

3. 高度  ```height:20px; ```

   高度可以写像素值：19px； 

   也可以写百分比值：20%；

4. 背景颜色 

   ```background-color:#0F2D4C```

5. 字体样式

   ```color：#FF0000；```字体颜色红色 

   ```font-size：20px;``` 字体大小

6. 红色 1 像素实线边框 

   ```border：1px ```solid red;

7. DIV 居中 

   ```
   margin-left: auto;
   margin-right: auto;
   ```
   
8. 文本居中： 

   ```text-align: center;```

9. 超连接去下划线 

   ```text-decoration: none;```

10. 表格细线 
    ```
    table { 
border: 1px solid black; /*设置边框*/ 
    border-collapse: collapse; /*将边框合并*/ 
}
    td,th {
border: 1px solid black; /*设置边框*/ 
    } 
```
11. 列表去除修饰 
    ```
    ul { 
list-style: none; 
    } 
```