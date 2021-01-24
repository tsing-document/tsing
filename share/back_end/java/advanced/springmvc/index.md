#### SpringMVC

# 目录

## 1.1 Spring MVC 概述
## 1.2 Spring MVC 优点
## 1.3 Spring MVC WEB开发步骤
## 1.4 Spring MVC 执行流程
## 1.5 Spring MVC 相关注解
## 1.6 Spring MVC 返回值

---

## 1.1 SpringMVC 概述
Spring Web MVC是基于Servlet API构建的原始Web框架，从一开始就包含在Spring框架中。它的正式名称`Spring Web MVC`来自于它的源模块(Spring-webmvc)的名称，但它更常见的名称是`Spring MVC`。

与`Spring Web MVC`并行，`Spring Framework 5.0`引入了一个响应式堆栈Web框架，它的名字`Spring WebFlux`也是基于它的源模块(Spring - WebFlux)。

## 1.2 Spring MVC 优点
todo:

## 1.3 Spring MVC WEB 开发步骤
- Idea创建web项目：
    - 1、创建项目： 
        - 【File】-【New】- 【Project...】
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-01.png)
        - 创建空项目，选择`Next`：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-02.png)
        - 填写项目名称和存放的路径：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-03.png)
        - 默认弹出一个选择框，选择完成之后，点击`Next`：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-04.png)
        - 这个时候又弹出新的窗口，填写我们的模块的名称和路径，点击`Next`：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-05.png)
        - 设置我们的maven配置：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-06.png)
        - 创建项目完成！
    - 2、查看创建好的项目的结构：
        - ![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/createNewProject-07.png)
- 项目的案例：
    - 项目我会放在`github`上。

## 1.4 Spring MVC 执行流程

![](https://cdn.jsdelivr.net/gh/tsing-dong/drawing.bed/java/advanced/springmvc/springmvc.png)



## 1.5 Spring MVC 相关注解

- @Controller
- @RequestMethod
- @RequestParam
- @ResponseBody

## 1.6 Spring MVC 返回值

- ModelAndView
    - 返回数据和跳转视图。
- String
    - 跳转视图。
- void
- Object

