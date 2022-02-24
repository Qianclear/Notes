# 第二个Maven工程

+ 创建约定目录

  ```
  HelloFriend
  |---src
  |---|---main
  |---|---|---java
  |---|---|---resources
  |---|---test
  |---|---|---java
  |---|---|---resources
  |---pom.xml
  ```

+ pom.xml内容

  ```xml
  <?xml version="1.0" ?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>maven</groupId>
      <artifactId>HelloFriend</artifactId>
      <version>0.0.1-SNAPSHOT</version>
  
      <name>HelloFriend</name>
      
      <dependencies>
          <!--这样一部分是依赖处理-->
          <dependency>
              <groupId>junit</groupId>
              <artifactId>junit</artifactId>
              <version>4.0</version>
              <scope>test</scope>
          </dependency>
          
          <!--因为用到了Hello里面的内容， 所以在这里处理依赖，感觉有点类似于导入的意思，import-->
          <dependency>
              <groupId>maven</groupId>
              <artifactId>Hello</artifactId>
              <version>0.0.1-SNAPSHOT</version>
              <scope>compile</scope>
          </dependency>
          
      </dependencies>
  </project>
  ```

+ 在src/main/java/maven(pom.xml文件中的<groupID>maven</groupID>)目录下新建HelloFriend.java文件

  ```java
  package maven;
  import maven.Hello;
  public class HelloFriend {
  	public String sayHelloToFriend(String name){
  		Hello hello = new Hello();
  		String str = hello.sayHello(name)+" I am "+this.getMyName();
  		System.out.println(str);
  		return str;
  	}
  	public String getMyName(){
  		return "John";
  	}
  }
  ```

  > 注意，这里用到了Hello工程，对于自己的工程一定要进行

+ 在src/test/java/maven目录下新建HelloFriendTest.java文件

  ```java
  package maven;	
  import static junit.framework.Assert.assertEquals;
  import org.junit.Test;
  import maven.Hello;
  
  public class HelloFriendTest {
  	@Test
  	public void testHelloFriend(){
  		HelloFriend helloFriend = new HelloFriend();
  		String results = helloFriend.sayHelloToFriend("litingwei");
  		assertEquals("Hello litingwei! I am John",results);	
  	}
  }
  ```

  > 像这里，如果直接mvn compile，估计不成功，报错信息应该是找不到Hello，虽然处理了依赖，但是我们还需要mvn install一下(在Hello文件里)

# Maven 其他知识

## 生命周期

1. 各个环节执行的顺序：不可打乱，必须按照既定的正确顺序执行

2. Maven的核心程序中定义了抽象的生命周期，生命周期中的各个阶段任务是由插件完成

3. Maven核心程序为了实现更好的自动化构建，无论现在要执行生命周期的哪一个阶段，都在生命周期最开始的位置开始执行，即从头开始

4. 插件和目标

   + 生命周期的各个阶段仅仅定义了要执行的任务是什么

   + 各个阶段和插件的目标是对应的

   + 相似的目标有特定的插件完成

     | 生命周期阶段 | 插件目标    | 插件                  |
     | ------------ | ----------- | --------------------- |
     | compile      | compile     | maven-compiler-plugin |
     | test-compile | testCompile | maven-compiler-plugin |

   + 可以将目标看作"调用插件功能的命令"

## 在Eclipse中使用Maven

1. Maven插件：Eclipse内置

2. Maven插件的设置

   <img src="ipic\1629358515075.png" alt="1629358515075" style="zoom:67%;" /><img src="ipic\1629358597302.png" alt="1629358597302" style="zoom:67%;" />

   + installations：指定Maven核心程序的位置，不建议使用插件自带的Maven程序，使用我们下载的

     > add -> 我们自己下载的文件夹

   + user settings：指定conf/settings.xml的位置，仅为获取本地仓库的位置

3. 基本操作

   + 创建Maven版的java工程

     > 注：可以Window -> Perspective -> Customize Perspective(自译：自定义透视) -> Menu Visibility 
     >
     > -> File -> New -> Maven Project，将Maven Project加入到菜单

     + new -> Maven Project -> **勾选”Create a simple project“**(创建简单工程，跳过典型选择)

     + 创建之后默认jre是1.5版本

     > 手动更改：右键-> build path -> Configure build path -> remove 1.5版本 -> add library
     >
     > -> jre System Library -> finish -> apply
     >
     > java compile -> 选择版本 -> apply
     >
     > 一劳永逸：打开pom.xml文件，找到<profiles>标签，插入
     >
     > ```xml
     >     <profile>
     >         <id>jdk-1.8</id>
     >         <activation>
     >             <activeByDefault>true</activeByDefault>
     >             <jdk>1.8</jdk>
     >         </activation>
     >         <properties>
     >             <maven.compiler.source>1.8</maven.compiler.source>
     >             <maven.compiler.target>1.8</maven.compiler.target>
     >             <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>
     >         </properties>
     >     </profile>
     > ```
     >
     > 

   + 创建Maven版的web工程

     + new -> Maven Project -> **勾选”Create a simple project“**(创建简单工程，跳过典型选择)-> 打包方式选择**war**

     > 此时，在eclipse看来依旧是java工程(相对于web工程，项目左上角没有小地球标志)

     + 右键工程 -> Properties -> Maven -> Project -> Facets->**去掉再勾上**Dynamic Web Module
   
       -> 选择新出现的**Further configuration available** -> Content directory里改为**src/main/webapp**
   
       > **一定要勾选Generate web.xml deployment descripto**，不然可能报错
       
     + 新建index.jsp文件，会报错，```javax.servlet.http.HttpServlet" was not found on the Java Build Path``` ，简而言之，就是**找不到包**了。此时复制包，然后ctrl+shift+t，粘贴，找到对应的包，然后在pom.xml里面加入对应的依赖即可
   
       ```xml
         <dependencies>
         	<dependency>
       		<groupId>javax.servlet</groupId>
       		<artifactId>servlet-api</artifactId>
       		<version>2.5</version>
       		<scope>provided</scope>
       	</dependency>
         </dependencies>
       ```
   
     + 此时部署的目录```Workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps\Webproject\WEB-INF\lib``` 里面为空
   
     + 再在xml文件里面加入
       ```xml
       	<dependency>
       		<groupId>log4j</groupId>
       		<artifactId>log4j</artifactId>
       		<version>1.2.17</version>
       	</dependency>
       ```
       
       > 没有特意说明，就默认为compile
       
     + 运行之后可以在部署目录里面发现```log4j-1.2.17.jar``` 文件说明compile参与部署
     
   + 执行Maven命令
   
     pom.xml右键选择.... 
     
   + 在Eclipse中导入手动建立的Maven工程
   
     + 右键import，**Exiting Maven Projects**(由于手动建立缺少.project等文件，故eclipse不认为他们是java工程，因而不选General里的Exiting Projects into Workspace)
   
       > 注意：由于导入Maven工程时，没有copy选项，所以Maven工程最好提前复制到workspace目录下，或者直接建立在workspace目录下

# 第三个Maven工程

1. new -> Maven Project -> **勾选”Create a simple project“** ->

   ​		groupId: maven
   ​		ArtifactId: MakeFriends
   ​		Package: maven

   然后finish

2. 在src/main/java包里面新建位于maven包里的MakeFriends文件

   ```java
   package maven;
   
   public class MakeFriends {
   	public String makeFriends(String name){
   		HelloFriend friend = new HelloFriend();
   		friend.sayHelloToFriend("litingwei");
   		String str = "Hey,"+friend.getMyName()+" make a friend please.";
   		System.out.println(str);
   		return str;
   	}
   }
   ```

   在src/test/java中新建位于maven包里的MakeFriendsTest文件

   ```java
   package maven;
   import static junit.framework.Assert.assertEquals;
   import org.junit.Test;
   public class MakeFriendsTest {
   	@Test
   	public void testMakeFriends(){		
   		MakeFriends makeFriend = new MakeFriends();
   		String str = makeFriend.makeFriends("litingwei");
   		assertEquals("Hey,John make a friend please.",str);
   	}
   }
   ```

   创立依赖

   ```xml
   <dependencies>
   	<dependency>
   		<groupId>junit</groupId>
   		<artifactId>junit</artifactId>
   		<version>4.9</version>
   		<scope>test</scope>
   	</dependency>
   	
   	<dependency>
   	   	<groupId>maven</groupId>
   	    <artifactId>HelloFriend</artifactId>
   	    <version>0.0.1-SNAPSHOT</version>
   	    <type>jar</type>
   	    <scope>compile</scope>
   	</dependency>
   </dependencies>
   ```

3. 此时，如果直接compile，失败。

   原因：所依赖的HelloFriend并没有打包安装好，所以找不到资源

   因此先maven install安装，此时就可以对该工程compile了
   
   > 看起来好像是挺麻烦的，但是maven一般是到了项目开发的最后，开发完了，将最终项目打包时使用

# 问题处理

## Maven install时出现No compiler is provided in this environment

``` [ERROR] No compiler is provided in this environment. Perhaps you are running on a JRE rather than a JDK? ```

1. 错误信息出现如上，这个环境没有提供编译器，可能你是在JRE上运行而不是JDK？

   因此我们可以将编译环境改为jdk

    Eclipse -> Window -> preferences -> Java -> install JREs -> add -> Standard VM -> next -> 选择jdk目录

   运行编译，哦，还是失败了

2. 好吧，问题没有得到解决，因此进行百度.....

   好的，经过百度，我知道前面的思路没毛病，但是不够，因为你还要对项目里面进行配置

   项目上右键 -> Build Path 后默认进入选项，找到Java Build Path，进入 Libraries，双击JRE System Library，**选择 Alternate JRE**(应该是代替的JRE)，选择对应的JDK，最后Finish即可

3. 好的此时再次进行maven install，成了