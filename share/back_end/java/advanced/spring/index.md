## 目录

- 一、Spring概述
- 二、核心思想IOC和AOP
- 三、Spring IOC应用
- 四、Spring AOP应用

---
### 一、Spring概述

#### 1.1 第一节 Spring 简介

- Spring是什么？
  
    - Spring是一个开源框架，由`Rod Johnson` 创建。它是为了解决企业应用开发的复杂性而出现。	
    
- Spring为什么会出现？
  
    - 因为当时EJB使用困难，所以Spring应世而生。
    
- Spring的核心的组件？

    |      核心模块名称      | 描述                                                         |
    | :--------------------: | :----------------------------------------------------------- |
    |       Spring IOC       | 包含了最为基本的Ioc容器BeanFactory的接口和实现，也就是说，在这个Spring的核心包中，不仅定义了IOC容器的最基本的接口（BeanFactory），也提供了一系列这个接口的实现，如XmlBeanFactory就是一个最基本的BeanFactory（IOC容器）。 |
    |       Spring Aop       | 这也是Spring的核心模块，围绕这个AOP的增强功能，Spring 集成了AspectJ作为AOP的一个特定实现，同时还在JVM动态代理、CGLIB的基础之上，实现了一个AOP框架。作为Spring集成其他模块的工具，比如`事务` 就是通过AOP集成到项目中的。 |
    |       Spring MVC       | Spring MVC 是以DispatcherServerlet为核心，实现了MVC模式，包括怎样和web容器环境的集成，web 请求的拦截、分发、处理和ModelAndView  数据的返回，以及如何集成各种UI视图展示和数据表现。 |
    | Spring JDBC/Spring ORM | Spring  JDBC主要封装了对数据库的操作。                                                                                                                                                            Spring ORM主要是将从数据库中查出来的数据，映射到对象中。 |
    |     Spring事务处理     | Spring 事务处理是一个通过Spring AOP实现自身功能增强的典型模块。 |
    |    Spring 远程调用     | Spring 为应用带来的一个好处就是能够将应用解耦。应用解耦，一方面可以降低设计的复杂性，另一方面，可以在解耦以后将应用模块分布式部署，从而提高系统整体的性能。 |
    |       Spring应用       | 从严格意义来说，这个模块不属于spring模块，这个部分是扩展的spring。 |

- Spring优点？

    - 低侵入式设计，代码的污染极低。
    - 将对象的管理交给框架处理，减低组件的耦合性。
    - 良好的提供了AOP技术。
    - 对主流框架的良好的整合和集成。

### 二、核心思想IOC和AOP

#### 2.1 什么是IOC?

- IOC是什么？
    - 控制反转（Inversion of Control,缩写为IOC）,是面向对象编程中的一种设计原则（思想）。不是设计实现。可以用来减少计算机代码之间的耦合度。
- IOC为什么会出现？
    - 因为如果对象让程序员管理的话，是一个噩梦，代码之间耦合程度非常庞大。所以IOC出现就是为了程序员不需要通过 `new`创建对象了，让框架帮我们管理对象的创建。
- IOC实现策略：
    - **依赖查找：**容器提供回调接口和上下文条件给组件。EJB和Apache Avalon 都使用这种方式。这样一来，组件就必须使用容器提供的API来查找资源和协作对象，仅有的控制反转只体现在那些回调方法上：容器将调用这些回调方法，从而让应用代码获得相关资源。
    - **依赖注入：**组件不做定位查询，只提供普通的Java方法让容器去决定依赖关系。容器全权负责的组件的装配，它会把符合依赖关系的对象通过JavaBean属性或者构造函数传递给需要的对象。通过JavaBean属性注射依赖关系的做法称为设值方法注入(Setter Injection)；将依赖关系作为构造函数参数传入的做法称为构造器注入（Constructor Injection）。
- todo:后面把oneNote中的图放进来。
- todo: DI这个要看看..

#### 2.2   什么是AOP？

- AOP是什么？
    - 面向切面编程（Aspect Oriented Programming，缩写为AOP），可以通过预编译方式和运行其动态代理实现在`不修改源代码`的情况下给程序动态统一添加功能。
- AOP为什么会出现？
    - 在开发的过程中多个模块之间有某段同样的代码，就需要通过面向切面来解决。

### 三、Spring IOC 应用

#### 3.1 Spring容器的组织结构图

#### 3.2 案例：把对象创建交给Spring

- 1、在`pom.xml`中引入依赖

    ```xml
    <dependency>
    	<groupId>org.springframework</groupId>
    	<artifactId>spring-context</artifactId>
    	<version>5.0.2.RELEASE</version>
    </dependency>
    ```

- 2、创建`bean.xml`

    - 注意：如果是`idea` 添加依赖一定添加我下面的依赖。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
    </beans>
    ```

- 3、创建实体类

    ```java
    public class Demo {
        private int id;
        private String name;
        public Demo() {
        }
        public Demo(int id, String name) {
            this.id = id;
            this.name = name;
        }
        public int getId() {
            return id;
        }
        public void setId(int id) {
            this.id = id;
        }
        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        @Override
        public String toString() {
            return "Demo{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
        }
    }
    ```

- 4、在`bean.xml`中配置我们的实体类

    ```xml
    <bean id="demo" class="com.tsing.spring.pojo.Demo">
    	<property name="id" value="1"/>
    	<property name="name" value="青衣"/>
    </bean>
    ```

- 5、测试类

    ```java
    public class ApiTest {
        public static void main(String[] args) {
            ApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean.xml");
            Demo demo = (Demo) applicationContext.getBean("demo");
            System.out.println(demo);
        }
    }
    ```

### 四、Spring AOP 应用

#### 4.1 概念

Spring实现AOP思想使用的是动态代理技术。

默认情况下，Spring 会根据被代理对象是否实现接口来选择使用JDK还是CGLIB。当被代理对象没有实现任何接口时，Spring会选择CGLIB。当被代理对象实现了接口，Spring会选择JDK官方的代理技术，不过我们可以通过配置的方式，让Spring强制使用CGLIB。

#### 4.2 案例Spring AOP 代码实现

- 注解方式：

    - 1、在`pom.xml`中引入依赖

        ```xml
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.1.12.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.4</version>
        </dependency>
        ```

    - 2、编写要被切面的类

        ```java
        public class BusinessCode {
            public void sayHello() {
                System.out.println("在我前面和后面加上护卫队，不然我会被刺杀的！");
            }
        }
        ```

    - 3、将要被切面的类，配置在`bean.xml`中

        ```xml
        <bean id="businessCode" class="com.tsing.spring.business.BusinessCode">
        </bean>
        ```

    - 4、编写切面类

        ```java
        @Component("annotationTest")
        @Aspect
        public class AnnotationTest {
            //定义切点
             @Pointcut("execution(* *.sayHello(..))")
             public void sayHello(){}
        
            //环绕通知。注意要有ProceedingJoinPoint参数传入。
            @Around("sayHello()")
            public void sayAround(ProceedingJoinPoint pjp) throws Throwable{
                System.out.println("护卫队开始集结。。。。");
                System.out.println("前护卫----注解类型环绕通知..环绕前");
                pjp.proceed();//执行方法
                System.out.println("后护卫----注解类型环绕通知..环绕后");
            }
        }
        ```

    - 5、编写测试类

        ```java
        public class ApiTest {
            @Test
            public void testAop() {
                ApplicationContext applicationContext = new ClassPathXmlApplicationContext("bean.xml");
                BusinessCode businessCode = (BusinessCode)applicationContext.getBean("businessCode");
                businessCode.sayHello();
            }
        }
        ```

        




​    

