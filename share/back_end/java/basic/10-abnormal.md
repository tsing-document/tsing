#### 异常

- 概要：
    - 异常体系：
        - ![collection](./img/exception.png)
    - 错误的方式：
        - 编译错误
        - 运行时错误
        - 逻辑错误
    - 异常的继承体系：
        - Throwable
            - Error
                - 虚拟机错误
                - 内存溢出
                - 线程锁死
            - Exception
                - IoException
                - RuntimeExption
                    - 空指针异常
                    - 数组下标越界异常
                    - 算数异常
                    - 类型转换异常
    - 异常分类：
        - 受查异常
            - IoException
                - 比如文件读取 FileInputStream
        - 非受查异常
            - Error
            - RuntimeExption
    - 异常处理：
        - 捕捉异常
        - 声明异常
            - 子类的声明异常的范围不能超过父类的声明范围。
    - 自定义异常
        - 封装
        - 快速定位
    - 堆栈的轨迹
- 语法：
    ```java
        //异常处理 - 捕捉异常
            try {
                //可能出现异常的代码
            } catch (Exception e) {
                e.printStackTeace();
            } finally {
                //都会执行
            }
        
        //异常处理 - 声明异常
            throws 抛出异常

    ```
- 案例：
    ```java
        //自定义异常
            package com.tsing.extend.demo5;
            /**
            * 
            * @author dongli
            * 自定义异常的步骤：
            * 	- 1.创建类
            *  - 2.继承 Exception 类或者 Exception 的子类
            *  - 3.重写构造方法
            */
            public class DemoException extends Exception{
                
                public DemoException() {};
                
                public DemoException(String message) {
                    super(message);
                };

            }

    ```
