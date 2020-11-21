# 内部类
- 概念：
    - 1.内部类：
        - 概念：
            - 就是在一个类中定义一个类。
        - 内部类的访问特点：
            - 内部类可以直接访问外部类的成员，包括私有。
            - 外部类要访问内部类的成员，必须创建对象。
    - 2.内部类-成员内部类：
        - 按照内部类在类中定义的位置不同，可以分为两种形式：
            - 在类的成员位置：成员内部类。
            - 在类的局部位置：局部内部类。
                - 局部内部类是在方法中定义的类，所以外界无法直接使用，需要在方法内部创建对象并使用。
                - 该类可以直接访问外部类的成员，也可以访问方法内的局部变量。
    - 3.匿名内部类：
        - 前提：
            - 存在一个接口或者类，这个的类可以是具体类也可以是抽象类。
- 语法：
    ```java
        //1.内部类：
            public class 类名 {
                修饰符 class 类名{

                }
            }

        //2.内部类-成员内部类：
            外部类名.内部类名 对象名 = 外部类对象.内部类对象；

        //3.匿名内部类：
            new 类名或者接口名() {
                重写方法；
            }    
    ```
- 案例：
    ```java
        //1.内部类：
            public class Outer {
                public class Inner {

                }
            }
        //2.内部类的访问特点：
            package com.tsing.extend.demo4;

            public class Outer {
                
                private int num = 10;
                
                //内部类访问外部类的成员。
                public class Inner {
                    public  void show() {
                        System.out.println(num);
                    }
                }
                
                //外部类访问内部类的成员。
                public void method() {
                    //show(); 错误方式
                    
                    Inner n = new Inner();
                    n.show();
                }
            }

        //3.内部类-成员内部类：
            //Outer类
                package com.tsing.extend.demo4;

                public class Outer {
                    
                    private int num = 10;
                    
                    //因为内部类是不想让别人调用，所以 public 是不实用的。
                    /*
                    public class Inner {
                            public  void show() {
                                System.out.println(num);
                            }
                        }
                    */
                    private class Inner {
                        public  void show() {
                            System.out.println(num);
                        }
                    }
                    
                    public void method() {
                        Inner i = new Inner();
                        i.show();
                    }
                    
                }
            //测试类
                package com.tsing.extend.demo4;

                public class InnerTest {
                    
                    public static void main(String[] args) {
                        //创建内部类，调用方法。下面这种方式不常用。
                        /**
                        * Outer.Inner oi = new Outer().new Inner();
                        * oi.show();
                        */
                        
                        Outer o = new Outer();
                        o.method();
                        
                    }
                }
        //4.内部类-局部内部类：
            //Outer
                package com.tsing.extend.demo4;

                public class Outer {
                    
                    private int num = 10;
                    
                    public void method() {
                        class Inner {
                            public void show() {
                                System.out.println(num);
                            }
                        }
                        
                        Inner i = new Inner();
                        i.show();
                    }
                    
                }
            //测试类
                package com.tsing.extend.demo4;

                public class OuterTest {
                    
                    public static void main(String[] args) {
                        
                        Outer o = new Outer();
                        o.method();
                        
                    }
                }

        //5.匿名内部类：
            //Outer
                package com.tsing.extend.demo4;

                public class Outer {
                    
                    public void method() {
                        Inter i = new Inter() {
                            @Override
                            public void show() {
                                System.out.println("匿名内部类");
                                
                            };
                        };
                        
                        i.show();
                    }
                    
                }
            
            //Inter
                package com.tsing.extend.demo4;

                public interface Inter {
                    
                    void show();

                }
            
            //OuterTest
                package com.tsing.extend.demo4;

                public class OuterTest {
                    
                    public static void main(String[] args) {
                        Outer o = new Outer();
                        o.method();
                    }
                }



    ```
