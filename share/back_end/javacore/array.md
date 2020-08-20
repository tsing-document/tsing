# 数组
- 概念：
    - 数组是一种数据结构，用来存储同一类型值的集合。同一个整型下标可以访问数组中的每一个值。
    - 在声明数组变量时，需要指出数组类型和数组变量的名字。
- 语法：
    ```java
        //1.数组
            /*
                声明数组
                    int[] a;

                初始化数组
                    int[] a = new int[100];

                简化初始化数组
                    String[] names = { "李栋", "王彦舒", "老子恨你" };
            */
    ```
- 案例：
    ```java
        int[] arr = new int[10];
        arr[0] = 3;
            for(int i = 0; i < arr.length; i++) {
                System.out.println(arr[i]);
            }
    ```

## todo: 多维数组
