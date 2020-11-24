#### 反射

- 概要：
    - 定义：
        - 获取class对象方式：
            - new ClassName().getClass()
            - ClassName.class
            - Class.forName("类的全路径");
    - 方法：
        - 构造器
        - 方法
        - 字段
        - JDK新增方法
    - 操作对象：
    - 调用方法：
    - 访问成员变量的值：
    
- 语法：
- 案例：
```java
    //获取class对象方式：
        package com.tsing.reflex;
        //获取类的方式
        public class ReflexDemo {
            public static void main(String[] args) {
                //第一种
                Demo d = new Demo();
                Class<? extends Demo> class1 = d.getClass();

                //第二种
                Class<Demo> class2 = Demo.class;

                //第三种
                try {
                    Class<?> class3 = Class.forName("com.tsing.reflex.Demo.java");
                } catch (ClassNotFoundException e) {
                    e.printStackTrace();
                }
            }
        }
    
    //方法
        //构造器
            package com.tsing.reflex;
            import java.lang.reflect.Constructor;

            public class ReflexDemo {
                public static void main(String[] args) {

                    Class<Demo> c2 = Demo.class;

                    //获取所有的构造
                    Constructor [] constructors = c2.getDeclaredConstructors();
                    for (Constructor co: constructors) {
                        System.out.println(co);
                    }

                    System.out.println("=====================================");

                    //获取public构造方法
                    Constructor [] constructors1 = c2.getConstructors();
                    for (Constructor co : constructors1) {
                        System.out.println(co);
                    }

                    System.out.println("=====================================");

                    //获取带有参数的构造方法,public修饰的private修饰的不能获取
                    try {
                        Constructor co = c2.getConstructor(int.class);
                        System.out.println(co.getName());
                    } catch (NoSuchMethodException e) {
                        e.printStackTrace();
                    }

                    System.out.println("=====================================");

                    //获取带有参数构造方法。
                    try {
                        Constructor<Demo> co = c2.getDeclaredConstructor(int.class, String.class);
                        System.out.println(co.getName());
                    } catch (NoSuchMethodException e) {
                        e.printStackTrace();
                    }
                }
            }

        //方法
            package com.tsing.reflex;
            import java.lang.reflect.Method;

            public class ReflexDemo {
                public static void main(String[] args) {

                    Class<Demo> c2 = Demo.class;

                    //获取所有的方法和修饰符无关
                    Method[] declaredMethods = c2.getDeclaredMethods();
                    for (Method declaredMethod : declaredMethods) {
                        System.out.println(declaredMethod);
                    }

                    System.out.println("==========================================");

                    //获取所有public方法
                    Method[] methods = c2.getMethods();
                    for (Method ms: methods) {
                        System.out.println(ms);
                    }

                    System.out.println("==========================================");

                    //获取指定形参的public方法
                    try {
                        Method method = c2.getMethod("function02", int.class, String.class);
                    } catch (NoSuchMethodException e) {
                        e.printStackTrace();
                    }
                }
            }
        
        //字段
            package com.tsing.reflex;
            import java.lang.reflect.Field;
            import java.lang.reflect.Method;

            public class ReflexDemo {
                public static void main(String[] args) {

                    Class<Demo> c2 = Demo.class;

                    //获取所有的字段，public
                    Field[] fs = c2.getFields();
                    for (Field field : fs) {
                        System.out.println(field);
                    }

                    System.out.println("===============================");

                    //获取指定字段，public
                    Field sex = null;
                    try {
                        sex = c2.getField("sex");
                        System.out.println(sex);
                    } catch (NoSuchFieldException e) {
                        e.printStackTrace();
                    }

                    System.out.println("===============================");

                    //获取指定的字段，访问权限无关
                    try {
                        Field id = c2.getDeclaredField("id");
                        System.out.println(id);
                    } catch (NoSuchFieldException e) {
                        e.printStackTrace();
                    }

                    System.out.println("===============================");

                    //获取所有的字段，访问权限无关
                    Field[] declaredFields = c2.getDeclaredFields();
                    for (Field declaredField : declaredFields) {
                        System.out.println(declaredField);
                    }
                }
            }

    //操作对象：
        package com.tsing.reflex;
        import java.lang.reflect.Constructor;
        import java.lang.reflect.InvocationTargetException;

        public class ReflexDemo {
            public static void main(String[] args) {

                Class<Demo> c2 = Demo.class;

                //方式一
                try {
                    Demo demo = c2.newInstance();
                    String dong = demo.funciton03("dong");
                    System.out.println(dong);
                } catch (InstantiationException e) {
                    e.printStackTrace();
                } catch (IllegalAccessException e) {
                    e.printStackTrace();
                }

                //方式二
                try {
                    Constructor<Demo> constructor = c2.getConstructor(int.class, String.class);
                    Demo instance = constructor.newInstance(1, "青衣");
                    System.out.println(instance);
                } catch (NoSuchMethodException | InstantiationException | IllegalAccessException | InvocationTargetException e) {
                    e.printStackTrace();
                }
            }
        }

    //调用方法
        package com.tsing.reflex;

        import java.lang.reflect.InvocationTargetException;
        import java.lang.reflect.Method;

        public class ReflexDemo {
            public static void main(String[] args) {

                Class<Demo> c2 = Demo.class;

                try {
                    Method method = c2.getMethod("function02", String.class);
                    method.invoke(c2.newInstance(), "执行方法");
                } catch (NoSuchMethodException | IllegalAccessException | InvocationTargetException | InstantiationException e) {
                    e.printStackTrace();
                }
            }
        }

```
