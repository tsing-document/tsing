![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/senior/distriuted/dubbo/basic/case/java-senior-distriuted-dubbo-%E5%9F%BA%E7%A1%80%E7%AF%87-helleworld.png)

# 目录
- 快速开始

## 1、快速开始

> 1、pom.xml 添加依赖
```java
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.1</version>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>dubbo</artifactId>
        <version>2.5.3</version>
    </dependency>
    <dependency>
        <groupId>com.101tec</groupId>
        <artifactId>zkclient</artifactId>
        <version>0.2</version>
    </dependency>
```

> 2、创建接口
```java
  public interface DemoService {
      String sayHello(String name);
  }
```

> 3、创建实现类
```java
  public class DemoServiceImpl implements DemoService {
    @Override
    public String sayHello(String name) {
        return "Hello " + name;
    }
}
```

> 4、创建配置文件 `rovider.xml`
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo" xmlns="http://www.springframework.org/schema/beans" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!-- 提供方应用信息，用于计算依赖关系 -->
    <dubbo:application name="demo-service-app"  />
    
    <!-- 使用zookeeper广播注册中心暴露服务地址 -->
    <dubbo:registry address="zookeeper://127.0.0.1:2181"/>

    <!-- 用dubbo协议在20880端口暴露服务 -->
    <dubbo:protocol name="dubbo" port="20880" />

    <!-- 声明需要暴露的服务接口 -->
    <dubbo:service interface="com.snails.demo.provioder.service.DemoService" timeout="3000" ref="demoService"/>

    <!-- 和本地bean一样实现服务 -->
    <bean id="demoService" class="com.snails.demo.provioder.service.impl.DemoServiceImpl" />
</beans>
```

> 5、创建服务启动类
```java
public class Provider {
    public static void main(String[] args) throws IOException {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext(new String[]{"provider.xml"});
        context.start();
        System.in.read(); // 按任意键退出
    }
}
```

> 6、创建配置文件`consumer.xml`
```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:dubbo="http://code.alibabatech.com/schema/dubbo" xmlns="http://www.springframework.org/schema/beans" xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">

    <!-- 消费方应用名，用于计算依赖关系，不是匹配条件，不要与提供方一样 -->
    <dubbo:application name="consumer"  />

    <!-- 使用multicast广播注册中心暴露发现服务地址 -->
    <dubbo:registry address="zookeeper://127.0.0.1:2181" />

    <!-- 生成远程服务代理，可以和本地bean一样使用demoService -->
    <dubbo:reference id="demoService" interface="com.snails.demo.provioder.service.DemoService" />
</beans>
```

> 7、创建服务启动类
```java
public class Consumer {
    public static void main(String[] args) throws Exception {
        ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("consumer.xml");
        context.start();
        DemoService demoService = (DemoService)context.getBean("demoService"); // 获取远程服务代理
        String hello = demoService.sayHello("world"); // 执行远程方法
        System.out.println( hello ); // 显示调用结果
    }
}

```


<span style="display:block;text-align:center;color:#DCDCDC;">-END-</span>
![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/personal/%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7.png)
您好，我是一个Java小白，希望和大家一起在技术的道路上一快快乐的学习。希望与您在网络的世界上会面。


