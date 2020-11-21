#### 面向对象

- 概要：
    - 封装：
        - 定义：
            - 隐藏对象内部的复杂性，只对外公开简单的接口。便于外界的调用，从而提高系统的可扩展性、可维护性。通俗的将，把该隐藏的隐藏起来，该暴露的暴露出来。
        - 封装的体现：
            - 我们将类的属性私有化(private),同时，提供公共的(public)方法获取(getXXX)和设置(setXXX)值。
            - 不对外暴露私有的方法。
        - 权限修饰符：
            - 4中权限修饰符：
                - private --> default --> protected --> public
                - private
                    - 类内部
                - default
                    - 类内部
                    - 同一个包
                - protected
                    - 类内部
                    - 同一个包
                    - 不同包的子类
                - public
                    - 类内部
                    - 同一个包
                    - 不同包的子类
                    - 同一个项目
            - 修饰的地方：
                - 可以修饰类和类的内部结构：属性、方法、构造器、内部类。
                - 4种修饰符能修饰：属性、方法、构造器、内部类。
                - 修饰类的话只能使用：default、public。
    - 继承：
        - 特点：
            - 1.子类可以拥有父类的内容。
            - 2.子类还可以拥有自己的专有的内容。
            - 3.在父子类的继承关系中，如果成员变量重名，则创建子类对象时，访问方式有两种方式：
                - 直接通过子类对象访问成员变量：
                    - 等号左边是谁，就优先用谁，没有则向上找。
                - 间接通过成员方法访问成员变量：
                    - 该方法属于谁，就优先用谁，没有则向上找。
            - 4.继承关系中重名的关系：
                - 局部变量：
                    - 直接写成员变量名。
                - 本类中的成员变量：
                    - this.成员变量名。
                - 父类中的成员变量：
                    - super.成员变量名。
            - 5.在父子类的继承关系中，创建子类对象，访问成员方法的规则：
                - 创建的对象是谁，就优先用谁，如果没有就向上找。
            - 6.重写：
                - 在继承关系中，方法名称一样，参数列表不同。覆盖
            - 7.重载：
                - 方法名称一样，参数列表不一样。
            - 8.构造方法：
                - 子类构造方法中默认隐含 `super()`，所以一定先调用父类的构造，后执行子类的构造。
                - 子类构造可以通过 `super` 关键字来调用父类重载构造。
                - super的父类构造调用，必须是子类构造方法的第一个语句。不能一个子类构造调用多次  `super` 构造。
                - 子类必须调用父类构造方法，不写则赠送 `super()`,写了则用写的指定的的 `super` 调用，`super`只能有一个，还必须是第一个。
        - 注意事项：
            - 无论成员方法和成员变量，都不会向下找。
            - 继承是多态的前提。
            - 阻止继承的方式是用 `final` 关键字修饰。
    - 多态：
        - 定义：
            - 多态是同一个行为具有不同的表现形式或形态的能力。
            - 一个对象拥有多种形态，这就是多态。
            - 代码中体现多态性，其实就是父类引用指向子类对象。 
        - 多态的必要条件：
            - 继承
            - 重写
            - 父类引用指向子类对象
- 语法：
```java
    //1.定义子类：
        public class Demo extends OldClass{

        }

    //2.继承：
        //定义：
            public class OldClass{

            }

            public class Demo extends OldClass{
        
            }

            //定义父类的格式：
            public class 父类名称 {
                // ...
            }

            //定义子类的格式：
            public class 子类名称 extends 父类名称 {

            }
    //3.多态：
        父类名称 对象名 = new 子类名称();
                    ||
        接口名称 对象名 = new 实现类名称();
```
- 案例：
```java
    //4.多态
        //Demo01Multi
            package com.tsing.extend.demo3;
            
            //代码中体现多态性，其实就是父类引用指向子类对象。 
            public class Demo01Multi {

                public static void main(String[] args) {
                    //多态写法
                    //左侧父类的引用指向右侧子类的对象
                    Fu obj = new Zi();
                    obj.method();
                    obj.methodFu();
                }

            }
                    
        //Fu
            package com.tsing.extend.demo3;

            public class Fu {

                public void method() {
                    System.out.println("父类方法执行");
                }
                
                public void methodFu() {
                    System.out.println("父类特有的方法！！！");
                }
            }

        //Zi
            package com.tsing.extend.demo3;

            public class Zi extends Fu {
                
                @Override
                public void method(){
                    System.out.println("子类方法执行！！！");
                }
            }
```
