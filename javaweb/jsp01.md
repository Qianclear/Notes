# jsp导

JSP（全称java Server Pages）是一种动态网页技术标准。

JSP部署于网络服务器上，可以响应客户端发送的请求，并根据请求内容动态地生成HTML、XML或其他格式文档的Web网页，然后返回给请求者。

> JSP技术以Java语言作为脚本语言，为用户的HTTP请求提供服务，并能与服务器上的其它Java程序共同处理复杂的业务需求。 

## JSP:动态网页

静态、动态:

不用和是否有“动感”混为--谈

是否随着时间、地点、用户操作的改变而改变

>  动态网页需要使用到服务端脚本语言(jSP)

## 架构

BS :Broswer Server

客户端可以通过浏览器 直接访问服务器

CS: Client Server

CS不足：

1. 如果然健升级，那么全部软件都需要升级
2. 维护麻烦：需要维护每一台客户端软件
3. 每一台客户端，都需要安装客户端软件

## tomcat解压后目录:

bin:可执行文件(startup. bat    shutdown. bat )
conf:配置文件(server. xml)
lib: tomcat依赖的jar文件
log:日志文件(记录出错等信息)
temp:临时文件
webapps: 可执行的项目(将我们开发的项目放入该目录)
work:存放由jsp翻译成的java,以及编辑成的class文件(jsp->java->class)

## 配置tomcat

+ 配置jdk (必须配置JAVA_ HOME) 
  java_ home classPath path
  
+ 配置catalina_ home
  双击bin/startup. bat启动tomacat
  
+ 常见错误: 可能与其他服务的端口号冲突
  tomcat端口号默认8080 (此端口号较为常见，容易冲突)，我修改此端口 (8848)
  
+ 此外，有可能在启动时出现乱码
  
  结局方法：tomcat目录->conf-> "**logging.properties**" 打开这个文本文件，找到如下配置项：
  
  java.util.logging.ConsoleHandler.encoding = UTF-8
  
  将 UTF-8 修改为 GBK，修改后的效果为：
  
  保存后，重启tomcat！

## 常见状态码:

| 200     | 一切正常                                      |
| ------- | --------------------------------------------- |
| 300/301 | 页面重定向 (跳转)                             |
| 404     | 资源不存在                                    |
| 403     | 权限不足 (如果访问a目录，但是a目录设置不可见) |
| 500     | 服务器内部错误(代码有误)                      |

创建项目时：必须要有

+ ROOT目录下的那个WEB-INF文件夹和web.xml文件
+ classes文件夹(放最终编译出来的class文件)
+ lib文件夹(放置jar包)(或者说是只有当前项目所需的jar包)

lib和classes文件夹都和web.xml在WEB-INF文件夹下

> jsp：在html中嵌套的java代码
>
> <%
>
> .....
>
> %>

> 在项目/WEB—INF/web.xml中设置默认的初始页面
>
> <welcome-file-list>
>
> ​    <welcome-file>index.jsp</welcome-file>
>
> </welcome-file-list>

## 虚拟路径

将web项目配置到webapps以外的目录

在conf文件夹里找到server.xml 文件，在文件的末尾吧，可以找到```<Host>.....</Host>``` 

> 这个是在<Engine>....</Engine>标签里面

在其中末尾处可以添加```<Context docBase="D:\developTools\JavaEE\apache-tomcat-9.0.46\webapps\JspProject" path="/JspProject" />```

docBase: 实际路径

path: 虚拟路径     （绝对路径**(文件的确切位置)**，相对路径**(相对于webapps)**）

缺点：需要重启

方式二：

在conf里的Catalina文件夹里localhost里新建立一个xml文件，名为“项目名.xml”，

> 当然，如果项目名改为ROOT，那么它就是默认的项目了

## 虚拟主机

这个没弄，大概意思是当你要访问一个网站时，电脑会先查询本机设置的域名ip并访问，如果没有的话，才去互联网查询访问

## JSP执行流程

jsp->java(Servlet文件) ->class

jsp 和servlet可以相互转换

> 因为第一次请求服务端会有翻译和编译的过程，所以比较慢，但是如果服务端修改了代码，则再次访问时会重新的翻译、编译。

> 如果出现了这个问题```The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build Path``` 说明是Javaweb工程下没有引入对应的library 
>
> 则 Window->Preferences->Server->RuntimeEnvironments->Add->选择Apache的版本后点Next，再填入安装的Apache Tomcat软件的安装目录 
>
> 然后右击web工程->Build Path->Configure buildpath->Java Build Path ->Libraries->Add Library->ServerRuntime->Next->Apache Tomcat Server->Finish->Apply and close

## 杂项

>WEB-INF中的文件无法通过客户端（浏览器）直接访问，只能通过请求转发来访问，但并不是所有的内部跳转都能访问WEB-INF；因为跳转有2种方式：请求转发 、重定向

**小发现：**

```
<body>
	
	hello index1!!....      jgh
	wulawulawula

</body>
```

以上代码片段的结论为：```  hello index1!!....      jgh	wulawulawula ```

嗯？？！！不对呀，电脑上显示的不是这样啊

是这样：

![1598097820424](ipic\1598097820424.png)

其实我本来先说编译器可能会选择性的忽略空格，现在看来，它可能没有忽略，只是显示的原因所以看不出空格的存在，而且可能在编译的时候，将换行替换为了```tab``` 

## 部署tomcat

在servers面板 新建一个 tomcat实例 ，  再在该实例中 部署项目（右键-add）
之后运行

注意：一般建议 将eclipse中的tomcat与 本地tomcat的配置信息保持一致： 将eclipse中的tomcat设为托管模式：【第一次】创建tomcat实例之后， 双击，选择Server Location的第二项

然而，我的第二项点不了，应该说三项都是点不了的灰色状态，可能因为这不是第一次创建吧

## JSP的页面元素

HTML  java代码（脚本Scriptlet）、指令、注释

1. 脚本Scriptlet

   ```
   <%
   		局部变量、java语句
   %>
   ```

   ```
   <%!
   		全局变量、定义方法
   %>
   ```

   ```
   <%=输出表达式 %>
   ```

一般而言，修改web.xml、配置文件、java  需要重启tomcat服务
但是如果修改 Jsp\html\css\js ，不需要重启



注意，out.println()不能回车； 要想回车：“<br/>”，即out.print() <%= %> 可以直接解析html代码

b.指令
page指令