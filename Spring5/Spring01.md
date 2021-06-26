# Spring5入门

> https://repo.spring.io/release/org/springframework/spring/

1. 打开idea，创建java普通工程new -> project ->java ->next ->Create... ->next ->...

2. 导入jar包，libs ->把spring里对应的beans、context、core、expression包复制创建新文件夹

   然后是一个commons-logging的日志文件，我没找到，就直接拉了一个资料里对应的文件。

   复制5个jar包，直接在project目录下新建的lib文件夹Ctrl+V

   然后file -> Project Structure...->Modules -> + ->1 JARs or directories ->找到对应的5个完成导入

3. 创建普通类，普通的方法

   ```
   public class User {
       public void add(){
           System.out.println("add......");
       }
   }
   ```

4.  创建Spring配置文件，在配置文件配置创建的对象 

   +  Spring配置文件使用xml格式 

     src 目录下新建xml文件

     ```
     <bean id ="user" class="spring5.User"></bean>
     ```

5.  进行测试代码编写 

   ```
       @Test
       public void testAdd(){
           //1.加载spring配置文件
           ApplicationContext context = new ClassPathXmlApplicationContext("bean1.xml");
           //2 获取配置创建的对象
           User user = context.getBean("user", User.class);
           System.out.println(user);
           user.add();
       }
   ```

   > 一定要进行导入

#  IOC

1. 什么是IOC
   + 控制反转(Inversion of Control)，把**对象创建**和对象之间的**调用过程**，交给**Spring进行管理**
   + 使用IOC目的：为了耦合度降低
   + 做入门案例就是IOC实现
   
   > 如果要在一个类中调用另一个类中的函数，采用在该类中创建对象并调用方法是原始的方法并且耦合度太高。或者采用工厂模式，即新建工厂类，在类里get函数里return new 对象(所需要用的类的对象)，再在原来的类里通过工厂调用
   > 
   > UserDao dao = UserFactory.getDao();
   >
   > dao.add();
   
   > 用IOC配置的话
   >
   > 1. 先xml配置文件，配置要创建的对象
   >
   > <bean id = "dao" class = "路径.UserDao"></bean>
   >
   > 2. 有services类和dao类，创建工厂类
   >
   >    String classValue = class的属性值;//这一步是xml解析
   >
   >    //通过反射创建对象
   >
   >    Class clazz= Class.forName(类的全路径，即为classValue);
   >
   >    return (UserDao) clazz.newInstance();

2. IOC底层原理

+ xml解析、工厂模式、反射 

3. IOC(**BeanFactory** 接口)

   > 1. IOC 思想基于 IOC 容器完成，IOC 容器底层就是对象工厂 
   >
   > 2. Spring 提供 IOC 容器实现两种方式：（两个接口） 
   >
   >    + BeanFactory：IOC 容器基本实现，是 Spring 内部的使用接口，不提供开发人员进行使用
   >
   >      **加载配置文件时候不会创建对象，在获取对象（使用）才去创建对象** 
   >
   >    + ApplicationContext：BeanFactory 接口的子接口，提供更多更强大的功能，一般由开发人员进行使用 
   >
   >      **加载配置文件时候就会把在配置文件对象进行创建**
   >
   >    一般来说都是使用第二种接口，因为直接把耗时的工作做完，这样响应快
   >
   >
   > 3. ApplicationContext 接口有实现类
   >
   >    选中ApplicationContext然后Ctrl+H，可以看到具体的实现类
   >
   >    FileSystemXMLApplicationContext
   >
   >    ClassPathXmlApplicationContext

   

# Bean管理

1. Bean管理含义：表示两个操作
   + Spring创建对象
   + Spring注入属性
2. Bean管理的操作
   + 基于xml配置文件方式实现
   + 基于注解方式实现

## xml方式

1. 基于xml方式创建对象

   ```
<bean id ="user" class="spring5.User"></bean>
   ```

   + 在 spring 配置文件中，使用 bean 标签，标签里面添加对应属性，就可以实现对象创建 
+ 在 bean 标签有很多属性，介绍常用的属性 
  
  + id 属性：获取对象的唯一标识 
   + class 属性：创建类全路径（包类路径）
     + name属性：与id属性的区别是可以加特殊符号比如"/"
   + 创建对象时候，默认也是执行无参数构造方法完成对象创建
  
2. 基于xml方式注入属性

   + DI：依赖注入，就是注入属性(DI是IOC的一种具体实现)

     1. 使用set方法进行注入

        + 创建类，定义属性和对应的 set 方法 

          ```
              //这个是set方法注入属性
              //创建属性
              private String bname;
              private String bauthor;
              //创建属性对应的set方法
              public void setBname(String bname) {
                  this.bname = bname;
              }
              public void setBauthor(String bauthor) {
                  this.bauthor = bauthor;
              }
          ```

        + 在 spring 配置文件配置对象创建，配置属性注入 

          ```
              <bean id="book" class="spring5.testdemo.Book" >
                  <!--  使用property完成属性注入
                      name：表示类里面属性的名称
                      value：表示向属性注入的值
                  -->
                  <property name="bauthor" value="2333"></property>
                  <property name="bname" value="QAQ"></property>
              </bean>
          ```
     
          
     
     2. 有参构造输入
     
        + 创建类，定义属性，创建属性对应有参数构造方法
     
          ```
          /**
           * 这个是采用有参构造注入属性
           */
          public class Orders {
          
              private String oname;
              private  String oaddress;
          
              public Orders(String oname, String oaddress) {
                  this.oname = oname;
                  this.oaddress = oaddress;
              }
          
          }
          ```
     
        + 在 spring 配置文件中进行配置
     
          ```
              <!--这个是有参构造注入属性-->
              <bean id="orders" class="spring5.Orders"><!--这里一开始会报错，是因为它一开始是默认无参构造，但是这里是有参构造，需用constructor-arg标签-->
                  <constructor-arg name="oname" value="asf"></constructor-arg>
                  <constructor-arg name="oaddress" value="Beijing"></constructor-arg>
          
              </bean>
          ```
     
          > ps:
          >
          > <constructor-arg>标签里还有一个index属性，表示索引值，value设为0表示为第一个参数
        
     3. p名称空间注入
     
        使用 p 名称空间注入，可以简化基于 xml 配置方式 
     
        + 添加 p 名称空间在配置文件中
     
          ```
              <!--    set方法注入属性-->
              <bean id="book" class="spring5.Book" p:bname="神秘力量" p:bauthor="001">
              </bean>
          ```
     
     4. 注入其他类型属性(特殊字符和空值)
     
        1. 字面量：在类里面为属性设置的固定值就是字面量
     
           空值
     
           ```
                   <property name="address">
                       <null/>
                   </property>
           ```
     
           特殊字符：这个可以参考html01.md里面的实体(转义字符串)
     
           另外如果属性值包含特殊字符一是可以选择转义，二是选择把带特殊符号的内容写在CDATA里面
     
           ```
                   <property name="address">
                       <value><![CDATA[厉害厉害]]>
                       </value>
                   </property>
           ```
     
           > 注意：在idea里面直接输入CD加回车即可直接调出<![CDATA[]]>
           >
           > 此外，个人还发现<![CDATA[]]>放在value标签里面时，<![CDATA[]]>前面如果有空格，输出的时候也会有空格，如果有换行，输出的时候也会有换行
     
        2. 注入属性—外部Bean
     
           创建两个类 service 类和 dao 类 
     
           在 service 调用 dao 里面的方法 
     
           在 spring 配置文件中进行配置 
           
           ```
               //先是创建UserDao属性，生成对应的set方法
               private UserDao userDao;
               public void setUserDao(UserDao userDao){
                   this.userDao = userDao;
               }
               public void add(){
                   System.out.println("service add .....");
                   userDao.update();
               }
           ```
           
           ```
               <!--创建service和dao的对象-->
               <bean id="UserService" class="spring5.service.UserService">
                   <!--注入UserDao属性
                   name：表示类里面的属性名称
                   ref：创建UserDao对象bean标签id值
                   因为是注入对象，所以是用ref
                   -->
                   <property name="userDao" ref="UserDaoImpl"></property>
               </bean>
               <bean id="UserDaoImpl" class="spring5.dao.UserDaoImpl"></bean>
           ```
           
           