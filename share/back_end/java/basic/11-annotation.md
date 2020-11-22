#### Annotation注解

- 概要：
    - 系统内置：
        - @Overrvide
        - @Deprecated
        - @SuppressWarnings
    - 自定义Annotation
    - 反射获取自定义Annotation
    - 扩展注解：
        - @Target
            - 指定注解使用的范围。
        - @Documented
            - 主要设置描述。
        - @Inhertied
            - 让子类继承注解。
- 语法：
```java
    //自定义Annotation
        //定义：
            [public]  @interface MyAnnotation {
            }
        //使用：
            @MyAnnotation
            public class AnnotationDemo {
            }
        //设置内容：
            //简单
            package com.tsing.annotation;

            public @interface MyAnnotation {
                public String value();
            }

            //升级
            public @interface MyAnnotation {
                public String name();
                public String age();
            }

            //高级
            public @interface MyAnnotation {
                public String[] name();
                public String age();
            }

            //超高级
            package com.tsing.annotation;

            public @interface MyAnnotation {
                public String[] name() default "tsing";
                public String age() default "34";
            }

            //特级
            package com.tsing.annotation;

            public enum MyName {
                TSING, DONG, QING
            }

            package com.tsing.annotation;

            public @interface MyAnnotation {
                public MyName name() default MyName.DONG;
                public String age() default "34";
            }

        //使用：
            //简单
            package com.tsing.annotation;

            @MyAnnotation(value = "test")
            public class AnnotationDemo {
            }

            //升级
            @MyAnnotation(name = "test", age = "43")
            public class AnnotationDemo {
            }

            //高级
            package com.tsing.annotation;

            @MyAnnotation(name = {"test"}, age = "43")
            public class AnnotationDemo {
            }

            //超高级
            package com.tsing.annotation;

            @MyAnnotation
            public class AnnotationDemo {
            }

            //特级
            package com.tsing.annotation;

            @MyAnnotation(name = MyName.QING, age = "45444")
            public class AnnotationDemo {
            }
        //设置Retention
            //使用
                @Retention(value = RetentionPolicy.RUNTIME)
                public @interface MyAnnotation {
                    public MyName name() default MyName.DONG;
                    public String age() default "34";
                }


```
- 案例：
```java
    //override
        package com.tsing.annotation;

        class Fu {
            public void sayHello() {
                System.out.println("这是一个父类方法！");
            }
        }

        class Zi extends Fu {
            @Override
            public void sayHello(){
                System.out.println("这是一个子类方法！");
            }
        }

        class OverrideAnnotation {
            public static void main(String[] args) {
                Zi z = new Zi();
                z.sayHello();
            }
        }
    //Deprecated
        package com.tsing.annotation;

        class Fu2{
            @Deprecated
            public void sayHello(){
                System.out.println("极客精神！");
            }
        }

        public class DeprecatedDemo1 {
            public static void main(String[] args) {
                Fu2 f = new Fu2();
                f.sayHello();
            }
        }
    //SuppressWarnings
        package com.tsing.annotation;

        import java.util.ArrayList;
        import java.util.List;

        public class SuppressWarningsDemo {
            List list = new ArrayList<>();

            public static void main(String[] args) {
            }

            @SuppressWarnings(value = "unchecked")
            public void sayHello() {
                list.add("test");
            }
        }
    //反射获取自定义Annotation
        package com.tsing.annotation;

        public class Fu3 {
            public void sayHello(){
                System.out.println("我是爸爸！");
            }
        }

        package com.tsing.annotation;

        public class DemoSimple extends Fu3{

            @Override
            @Deprecated
            @SuppressWarnings(value = "unchecked")
            @MyAnnotation
            public void sayHello() {
                System.out.println("test");
            }
        }

        package com.tsing.annotation;

        import java.lang.annotation.Annotation;
        import java.lang.reflect.Method;

        public class Demo {
            public static void main(String[] args) throws NoSuchMethodException {
                DemoSimple d = new DemoSimple();
                Class<? extends DemoSimple> c = d.getClass();

                Method toMe = c.getMethod("sayHello", new Class[] {});
                Annotation[] annotations = toMe.getAnnotations();

                if(toMe.isAnnotationPresent(MyAnnotation.class)) {
                    MyAnnotation ma = null;
                    ma = toMe.getAnnotation(MyAnnotation.class);
                    String age = ma.age();
                    System.out.println(age);
                    MyName name = ma.name();
                    String name1 = name.name();
                    System.out.println(name1);
                }
            }
        }
```
