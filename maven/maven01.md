# Maven是什么

Maven是一款服务于java平台的自动化构建工具

## 1. 构建

+ 概念：以"Java源文件"、"框架配置文件"、"JSP"、"HTML"、"图片"等资源为"原材料" ，去生产一个可以运行的项目的过程

  > 个人感觉类似于vuepress的一个build过程，像"打包"一样

  > 新发现，java的project里面有一个build文件夹，里面正是编译得到的字节码文件

  + 编译 + 部署 + 搭建

+ 编译：源文件—> 编译 —> class字节码文件—>交给JVM去执行

+ 部署：一个BS项目最终运行的并不是动态web工程本身，而是这个web工程"编译的结果"

  > 生的鸡——> 处理——> 熟的鸡
  >
  > 动态web工程——> 编译、部署——> 编译结果

## 2. 构建中的环节(了解)

1. 清理：将以前编译得到的旧的class字节码文件删除，为下一次编译做准备
2. 编译：将java源程序编程成class字节码文件
3. 测试：自动测试，自动焦勇Junit程序
4. 报告：测试程序执行结果
5. 打包：动态web工程打包成war包，java工程打jar包
6. 安装：Maven特定概念——将打包得到的文件复制到"仓库"中的指定位置
7. 部署：将动态web工程生成的war包复制到Servlet容器的指定目录下，使其可以运行

# 安装Maven核心程序

## 1. 检查**JAVA_HOME**环境变量

> 可以用命令行，输入
>
> echo %JAVA_HOME%

![1628067657787](ipic\1628067657787.png)

## 2. 解压Maven核心程序的压缩包

放在**非中文无空格**目录下

<img src="ipic\1628068139989.png" alt="1628068139989" style="zoom:80%;" />

## 3. 配置Maven环境变量

+ MAVEN_HOME或M2_HOME

  > 以普遍性而言，用这俩哪一个都行
  >
  > 但是据说，用M2_HOME可以避免一些犄角旮旯的错误....

  M2_HOME

  <img src="ipic\1628069858282.png" alt="1628069858282" style="zoom:67%;" />

  PATH

  <img src="ipic\1628069746351.png" alt="1628069746351" style="zoom:67%;" />

## 4. 验证

运行mvn -v查看Maven版本

<img src="ipic\1628070041293.png" alt="1628070041293" style="zoom:80%;" />

## 5. Maven的核心概念

1. 约定的目录结构
2. POM
3. 坐标
4. 依赖
5. 仓库
6. 生命周期/插件/目标
7. 继承
8. 聚合

# 第一个Maven工程

+ 创建约定的目录结构

  ```
  Hello
  |---src
  |---|---main
  |---|---|---java
  |---|---|---resources
  |---|---test
  |---|---|---java
  |---|---|---resources
  |---pom.xml
  ```

  + 根目录：工程名
  + src目录：源码
  + pom.xml文件：maven工程的核心配置文件
  + main目录：存放主程序
  + test目录：存放测试程序
  + java目录：存放java文件
  + resources目录：存放框架或者其他工具的配置文件

+ 如果想让自定义东西让框架或者工具知道，2种方法

  + 以配置的方法明确告诉框架

    ```xml
    <param-value>classpath:spring-context.xml</param-value>
    ```

  + 遵守框架内部已经存在的约定

    ```
    log4j.properties    //帮助控制台打印日志，之后会接触，必须有
    log4j.xml
    ```

  + 编码界共识：约定 > 配置 > 编码

+ pom.xml内容

  ```xml
  <?xml version="1.0" ?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  	<modelVersion>4.0.0</modelVersion>
  
  	<groupId>maven</groupId>
  	<artifactId>Hello</artifactId>
  	<version>0.0.1-SNAPSHOT</version>
      <!--这个是坐标，唯一标识-->
  
  	<name>Hello</name>
      <!--这个是工程名-->
  	  
  	<dependencies>
  		<dependency>
  			<groupId>junit</groupId>
  			<artifactId>junit</artifactId>
  			<version>4.0</version>
  			<scope>test</scope>
  		</dependency>
          <!--这个是依赖的其他jar包-->
  	</dependencies>
  </project>
  ```

  > 注：xml文件仅仅可以使用html的注释，即<!--注释内容-->

+ 在src/main/java/maven(pom.xml文件中的<groupID>maven</groupID>)目录下新建Hello.java文件

  ```java
  package maven;
  public class Hello {
  	public String sayHello(String name){
  		return "Hello "+name+"!";
  	}
  }
  ```

+ 在src/test/java/maven目录下新建HelloTest.java文件

  ```java
  package maven;	
  import org.junit.Test;
  import static junit.framework.Assert.*;
  //静态引入，可以调用所有的静态资源
  public class HelloTest {
  	@Test
  	public void testHello(){
  		Hello hello = new Hello();
  		String results = hello.sayHello("litingwei");
  		assertEquals("Hello litingwei!",results);
          //asser意为断言，函数意思为断言相等，返回值取决于是否相等
  	}
  }
  ```

## 常用Maven命令

> 注：执行与构建相关的Maven命令，必须进入pom.xml所在的目录
>
> 与构建相关：编译、测试、打包......

| 指令             | 作用         |
| ---------------- | ------------ |
| mvn clean        | 清理         |
| mvn compile      | 编译主程序   |
| mvn test-compile | 编译测试程序 |
| mvn test         | 执行测试     |
| mvn package      | 打包         |
| mvn install      | 安装         |
| mvn site         | 生成站点     |

> 注：执行mvn compile时可能会失败
>
> <img src="ipic\1628148586492.png" alt="1628148586492" style="zoom:100%;" />
>
> 去官网看看
>
> <img src="ipic\1628149130899.png" alt="1628149130899" style="zoom:80%;" />
>
> 看网上说是Maven和java的版本不匹配导致的，所以直接下载最新版的然后重新配置一下
>
> <img src="ipic\1628237272078.png" alt="1628237272078" style="zoom:67%;" />
>
> 很好，经过尝试，成功了
>
> 此时，

## 注：

1. Maven核心程序仅仅定义了抽象的生命周期，但具体工作必须由特点定插件完成，而插件本身并不在Maven核心程序中

2. 当需要用到插件时，会到先本地仓库(默认：C:\\Users\\[用户名]\\.m2\\repository)中进行查找

   > 修改默认仓库：
   >
   > + Maven解压目录\conf\settings.xml
   > + 找到localRepository标签，并将里面的<localRepository>/path/to/local/repo</localRepository>取出，并修改标签内容为已准备好的仓库
   >
   > <img src="ipic\1628239038197.png" alt="1628239038197" style="zoom:80%;" />

3. 当未查找到时，会自动连接外网，到中央仓库下载。

## POM

1. **Project Object Model** 项目对象模型

   DOM **Document Object Model** 文档对象模型

2. pom.xml对于maven工程是核心配置文件，可在文件中进行构建过程中的一切配置

   重要程度相当于web.xml对于动态web工程

## 坐标

用三个向量在仓库中定位一个Maven工程

1. groupid：公司或组织域名的倒序 + 项目名

   > <groupid>com.cqq.maven</groupid>

2. artifactid：模块名

   > <artifactid>Hello</artifactid>

3. version：版本号

   > <version>1.2.3</version>

```
  <groupId>org.springframework</groupId>
  <artifactId>spring-core</artifactId>
  <version>4.1.1.RELEASE</version>
```

```
org/springframework/spring-core/4.1.1.RELEASE/spring-core-4.1.1.RELEASE.jar
```

## 仓库

分类：

1. 本地仓库：当前电脑上部署的仓库目录，为当前电脑上所有的Maven工程服务

2. 远程仓库

   + 私服：搭建在局域网环境，服务局域网范围内的Maven工程

   + 中央仓库：搭建在Internet上，服务全世界所有的Maven工程

   + 中央仓库镜像：用于分档中央仓库流量，提升用户访问速度

     > 感觉像github的镜像，我记得是：https://hub.fastgit.org/

> 仓库中保存的是Maven工程，包括Maven自身所需要的插件，第三方框架或工具的jar包以及自己开发的Maven工程

## 依赖[初级]

+ Maven解析依赖信息时会到本地仓库中查找被依赖的jar包

  我们自己开发的Maven工程，使用mvn install命令安装后就可以进入仓库

  <img src="ipic\1629339042921.png" alt="1629339042921" style="zoom:75%;" />

+ 依赖范围

  | 范围依赖           | compile     | test   | provide         |
  | ------------------ | ----------- | ------ | --------------- |
  | 对主程序是否有效   | 有效        | 无效   | 有效            |
  | 对测试程序是否有效 | 有效        | 有效   | 有效            |
  | 是否参与打包       | 参与        | 不参与 | 不参与          |
  | 是否参与部署       | 参与        | 不参与 | 不参与          |
  | 典型例子           | spring-core | Junit  | servlet-api.jar |

  