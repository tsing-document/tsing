# 循环
- 概念：
    ```java
        //1.while

        //2.do...while...

        //3.for

        //4.增强for
    ```
- 语法：
    ```java
        //1.while
            while( 布尔表达式 ) {
                //循环内容
            }

        //2.do...while...
            //循环至少执行一次
            do {
                //循环内容
            } while(条件表达式);

        //3.普通for循环
            for(初始化; 布尔表达式; 更新) {
                //执行代码块
            }

        //4.增强for
            for(声明语句 : 表达式) {
                //执行代码块
            }

    ```
- 案例：
    ```java
        //1.while
            public static void main (String[] args) {
                int x = 10;
                while(x < 20) {
                    System.out.print("value of x : " + x );
                        x++;
                    System.out.print("\n");
                }
            }
        //2.do...while...
            public static void main (String[] args) {
                int x = 10;
                do{
                    System.out.print("value of x : " + x );
                        x++;
                    System.out.print("\n");
                } while (x < 12);
            }

        //3.for
            public static void main (String[] args) {
                for(int i = 0; i <= 10; i++){
                    System.out.println("执行了第" + i + "次");
                }
            }

        //4.增强for
            public static void main (String[] args) {
                String[] names = { "李栋", "王彦舒", "老子恨你" };
                for( String name : names ) {
                    System.out.println(name);
                };
            }
    ```
