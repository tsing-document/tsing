# 枚举
- 概念：
    - 定义：
        - 枚举就是要让某个类型的变量的取值只能为某个固定的值中的一个，枚举可以让编译器在编译时就可以控制源程序赋给的非法值。
- 语法：
- 案例：
    ```java
        //基础
            //ColorEnum
                package com.tsing.extend.demo10;

                public enum ColorEnum {
                    
                    RED,
                    GREEN,
                    BULE,

                }
            //测试类
                package com.tsing.extend.demo10;

                import java.util.Arrays;

                public class Demo {
                    
                    public static void main(String[] args) {

                        System.out.println(ColorEnum.BULE);
                        
                        ColorEnum[] tempce = ColorEnum.values();
                        
                        System.out.println(Arrays.toString(tempce));

                    }

                }

        //带构造的枚举
            //ColorEnum
                package com.tsing.extend.demo10;

                public enum ColorEnum {
                    
                    RED(10), GREEN(10), BULE(10);
                    
                    private int color;
                    
                    private ColorEnum () {
                        System.out.println("无参构造");
                    }
                    
                    private ColorEnum(int color) {
                        this.color = color;
                        System.out.println("有参构造");
                    }
                }

            //测试类
                package com.tsing.extend.demo10;
                public class Demo {
                
                    public static void main(String[] args) {

                        System.out.println(ColorEnum.RED);

                    }

                }
        
        //枚举实现接口
            //ColorEnum
                package com.tsing.extend.demo10;

                public enum ColorEnum implements Info{
                    
                    RED(10), GREEN(10), BULE(10);
                    
                    private int color;
                    
                    private ColorEnum () {
                        System.out.println("无参构造");
                    }
                    
                    private ColorEnum(int color) {
                        this.color = color;
                        System.out.println("有参构造");
                    }

                    @Override
                    public int getColor() {
                        return color;
                    }

                }
            //Info 接口
                package com.tsing.extend.demo10;

                public interface Info {
                    public int getColor();
                }
            
            //测试类
                package com.tsing.extend.demo10;
                public class Demo {
                    
                    public static void main(String[] args) {
                        System.out.println(ColorEnum.RED.getColor());

                    }

                }





    ```
