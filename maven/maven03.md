# 依赖[高级]

## 1.依赖的传递性

测试：在Hello项目的pom.xml文件中加入以下依赖

```xml
        <dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-core</artifactId>
			<version>4.0.0.RELEASE</version>
			<scope>compile</scope>
		</dependency>
```

我们会发现Hello、HelloFriend、MakeFriends的运行环境里，都有了改变

<img src="ipic\1629790890669.png" alt="1629790890669" style="zoom: 67%;" /><img src="ipic\1629790943790.png" style="zoom:67%;" /><img src="ipic\1629791159157.png" alt="1629791159157" style="zoom:67%;" />
在Hello里面添加依赖，由于HelloFriend依赖于Hello，故也出现了对应的spring-core等包，传递性由此看出

同时，我们也可以在Dependency Hierarchy(依赖层次)里看到对应的依赖关系

![1629791530279](ipic\1629791530279.png)

好处：对于可以传递的依赖，直接在最底层声明一次即可， 无需重复声明依赖

注意：非compile范围的依赖不能传递(可以理解为test 和provided 范围都是给自己用的，不进行传递 )

## 2.依赖的排除

1. 当被传递来的jar包里有不稳定的，不希望加入到当前工程中的jar包时，而你又无法修改，此时就需要排除掉

2. 排除方式

   在你当前项目中，对不需要的jar包所在的依赖中，加入

   ```xml
   <exclusions>
   	<exclusion>
   		<groupId></groupId>
   		<artifactId></artifactId>
   	</exclusion>
   </exclusions>
   ```

   进入Dependency Hierarchy，右键你不需要的jar包，选择Open POM，再进入Overview中，将对应的groupId和artifactId填入xml文件即可。

   <img src="ipic\1629795101566.png" alt="1629795101566" style="zoom:67%;" />

   > 此时，如果后来的项目依赖了这个项目，那么这个项目所排除的依赖，也会被后来的项目排除

## 3.依赖的原则

1. 作用：解决模块工程质检的jar包冲突问题

2. "路径"最短者优先

3. 路径相同时，先声明优先

   > 先声明指的是dependency标签的声明顺序

## 4. 同意管理依赖的版本

1. 假设当前有依赖有多个4.0.0版本的Spring各个jar包

   如果需要统一升级为4.1.1，手动逐一修改不可靠

2. 建议配置方式

   + 在properties标签内使用自定义标签统一声明版本号
   + 在需要统一版本的位置，使用${自定义标签名} 引用声明的版本号

   ```xml
   <properties>
   	<Q.spring.version>4.0.0.RELEASE</Q.spring.version>
   </properties>
   ```

   ```xml
   <version>${Q.spring.version}<version>
   ```

   + properties标签配合自定义标签声明的数据配置，同样可以使用于统一声明后再引用的场合

   ```xml
   <properties>
   	<Q.spring.version>4.0.0.RELEASE</Q.spring.version>
   	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   ```

# 继承

## 1.情景设定

Hello依赖的Junit：4.0

HelloFriend依赖的Junit：4.0

MakeFriends依赖的Junit：4.9

由于**test**范围的依赖**不能传递**，所以必然会分散在各个模块工程中，很容易造成版本的不一致

## 2. 需求

统一管理各个模块工程中对于Junit依赖的版本

## 3.思路

将Junit依赖统一提取到"父"工程中，在子工程中声明Junit依赖时，**不指定版本**，以"父"工程中的声明为准。同时也便于修改

## 4.步骤

1. 创建一个Maven工程作为父工程。注意：打包方式为pom

   ```xml
     <modelVersion>4.0.0</modelVersion>
     <groupId>maven</groupId>
     <artifactId>Parent</artifactId>
     <version>0.0.1-SNAPSHOT</version>
     <packaging>pom</packaging>
   ```

2. 在子工程中声明对父工程的引用

   ```
       <parent>
       	<groupId>maven</groupId>
     		<artifactId>Parent</artifactId>
     		<version>0.0.1-SNAPSHOT</version>
     		
     		<!-- 以当前文件为基准的父工程pom.xml文件的相对路径 -->
     		<relativePath>../Parent/pom.xml</relativePath>
     		
       </parent>
   ```

   

3. 将子工程的坐标中与父工程坐标中的重复内容删除

   <img src="ipic\1629799187589.png" alt="1629799187589" style="zoom:67%;" />

4. 在父工程中统一Junit的依赖

   ```xml
     <!-- 配置依赖的管理 -->
     <dependencyManagement>
     	<dependencies>
     		<dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.0</version>
               <scope>test</scope>
       	</dependency>
     	</dependencies>
     </dependencyManagement>
   ```

5. 在子工程中删除Junit依赖的版本号部分

   <img src="ipic\1629799111547.png" alt="1629799111547" style="zoom:67%;" />

6. 配置继承后，执行安装命令后，要先安装父工程，否则无法安装子工程

# 聚合

## 1.作用

用于"一件安装"各个模块工程

## 2. 配置方式

在一个"总的聚合工程" 中配置各个参与聚合的模块(可以是父工程)

```xml
  <modules>
  	<module>../Hello</module>
  </modules>
```

## 3.使用方式

在聚合工程的pom.xml上右键-> run as -> maven install