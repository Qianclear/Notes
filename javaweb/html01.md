# 基本知识

## html

基本格式：

```
<!-- 
	html根标签，一个页面中有且只有一个根标签，网页中的所有内容都应该写在html根标签中
-->
<html>
    <!-- head标签，该标签中的内容，不会在网页中直接显示，它用来帮助浏览器解析页面的-->
    <head>
        <!-- 
			title网页的标题标签，默认会显示在浏览器的标题栏中
				搜索引擎在检索页面时，会首先检索title标签中的内容
				它是网页中对于搜索引擎来说最重要的内容，会影响到网页在搜索引擎中的排名
		-->
        <title>我果然很帅，连浏览器都这么认为</title>
    </head>
    <!--body标签用来设置网页的主体内容，网页中所有可见的内容，都应该在body中编写-->
    <body>
        <!--
        这个结构体内部全都是注释，不会显示，但查看源码还是可以看到的
        -->
        <!-- 
			属性：
				可以通过属性来设置标签如果处理标签中的内容
				可以在开始标签中添加属性
				属性需要写在开始标签中，实际上就是一个名值对的结构
				属性名 = "属性值"，一个标签中可以同时设置多个属性，属性之间需要使用空格隔开
		-->
        <h1>  我真<font color="purple" size="7">帅</font>啊！！</h1>
    </body>

</html>
```

**文档注释：**

**doctype**

为了让浏览器知道我们使用的HTML版本，需要在网页最上边添加一个doctype声明，来告诉浏览器网页的版本。

对于HTML5来说直接```<!doctype html>``` 

> 如果不写文档声明，则会导致有些浏览器会进入一个怪异模式

> 进入怪异模式以后，浏览器解析页面会导致页面无法正常显示，所以为了避免进入该模式，一定要写文档声明

## 一些定义

**元素：** 一个完整的标签。

> 我们可以将元素和标签认为是近义词

```
<h1>一级标题</h1>                  h1即为元素

<p>我是一个<em>段落</em></p>        p为元素，em为p的子元素，p为em的父元素
```

```ANSI  自动以系统的默认编码来保存文件``` 

## 标签
1. 标签的格式: <标签名>封装的数据</标签名> 

2. 标签名大小写不敏感。 

3. 标签拥有自己的属性。

   + 分为基本属性：bgcolor="red" 可以修改简单的样式效果 

   + 事件属性： onclick="alert('你好！');" 可以直接设置事件响应后的代码。

4. 标签又分为，单标签和双标签。
   + 单标签格式： <标签名 /> br 换行 hr 水平线 
   + 双标签格式: <标签名> ...封装的数据...</标签名>

### 常用标签介绍

#### 标题标签

在HTML中，一共有六级标题标签

> h1 ~ h6
> 在显示效果上h1最大，h6最小，但是文字的大小我们并不关心
> 使用HTML标签时，关心的是标签的语义，我们使用的标签都是语义化标签

> 6级标题中，h1的最重要，表示一个网页中的主要内容，h2 ~ h6重要性依次降低
>
> 对于搜索引擎来说，h1的重要性仅次于title，搜索引擎检索完title，会立即查看h1中的内容

> h1标签非常重要，它会影响到页面在搜索引擎中的排名，页面只能写一个h1

| 标签    | 作用                                                 |
| ------- | ---------------------------------------------------- |
| <p></p> | p标签，用来表示一个段落                              |
| <br />  | br标签来表示一个换行                                 |
| <hr />  | hr标签也是一个自结束标签，可以在页面中生成一条水平线 |

#### font

> font 标签是字体标签**,**它可以用来修改文本的字体**,**颜色**,**大小**(**尺寸**) 
>
> color 属性修改颜色
>
> face 属性修改字体 
>
> size 属性修改文本大小

```<font color="red" face="宋体" size="7">我是字体标签</font>```

> ps：size 7 是最大的字号

实体(转义字符串)

| &实体字符; | 作用         |
| ---------- | ------------ |
| lt         | &lt;         |
| gt         | &gt;         |
| nbsp       | 表示空格     |
| copy       | 版权符&copy; |
| quot       | &quot;       |
| amp        | &amp;        |
| reg        | &reg;        |
| trade      | &trade;      |

### 图片标签

**img**：向网页中引入一个外部图片

**src** ：设置一个外部图片的路径

**alt**：用来设置在图片不能显示时，对图片的描述

> 搜索引擎可以通过alt属性来识别不同的图片
>
> 如果不写alt属性，则搜索引擎不会对img中的图片进行收录

**width**：可以用来修改图片的宽度,一般使用px作为单位

**height** ：可以用来修改图片的高度，一般使用px作为单位

> 宽度和高度两个属性如果指设置一个，另一个也会同时等比例调整大小
>
> 如果两个值同时指定则按照你指定的值来设置
>
> 一般开发中除了自适应的页面，不建议设置width和height 

**src**属性配置的是图片的路径，目前我们所要使用的路径全都是相对路径。

**相对路径：**

相对路径指相对于当前资源所在目录的位置

```<img src="abc/bcd/2.gif" alt="这是一个大松鼠"/>```

可以使用../来返回一级目录,返回几级目录就写几个../  

```<img src="../../img/2.gif" alt="这是一个大松鼠"/>```

**绝对路径：**

正确格式是**: http://ip:port/**工程名**/**资源路径

#### 图片格式

 **JPEG(JPG)**

> JPEG图片支持的颜色比较多，图片可以压缩，但是不支持透明
>
> 一般使用JPEG来保存照片等颜色丰富的图片

 **GIF**

> GIF支持的颜色少，只支持简单的透明，支持动态图
>
> 图片颜色单一或者是动态图时可以使用gif

**PNG**

> PNG支持的颜色多，并且支持复杂的透明
>
> 可以用来显示颜色复杂的透明的图片

**图片的使用原则**

> 效果不一致，使用效果好的

> 效果一致，使用小的

### 列表标签

+ ul 是无序列表 

+ li 是列表项

+ type 属性可以修改列表项前面的符号

  ```
      <ul type="none">
          <li>fist</li>
          <li>second</li>
      </ul>
      <ul>
          <li>fist</li>
          <li>second</li>
    </ul>
      <ol>
          <li>0000</li>
          <li>1111</li>
      </ol>
  ```
  
  

### meat

使用meta标签还可以用来设置网页的关键字

```<meta name="keywords" content="HTML5,JavaScript,前端,Java" />```

> 其中，name是对content的描述

> 还可以用来指定网页的描述

> 搜索引擎在检索页面时，会同时检索页面中的关键词和描述，但是这两个值不会影响页面在搜引擎中的排名

使用meta可以用来做请求的重定向

```<meta http-equiv="refresh" content="秒数;url=目标路径" />```

```<meta http-equiv="refresh" content="5;url=http://www.baidu.com" />```

> ps Ctrl + Shift + / = 快捷注释