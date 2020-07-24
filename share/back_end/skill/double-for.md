# 双重 for 循环打印出你想要的任何形状
- hello world：
    - 说明：
        - 直观的看出双重 `for` 执行策略
    - 代码：
        ```java
            package com.tsing.algorithm.dichotomysearch;

            public class DoubleFor {
                
                public static int[] doblueFor(String[] arg1,String[] arg2) {
                    for (int i = 0; i < arg1.length; i++) {
                        for (int j = 0; j < arg2.length; j++) {
                            System.out.println(arg1[i] + arg2[j]);
                        }
                    }
                    return null;
                }
                
                public static void main(String[] args) {
                    String[] arg1 = {"外层-第一个", "外层-第二个", "外层-第三个"};
                    String[] arg2 = {"内层-第一个", "内层-第二个", "内层-第三个"};
                    doblueFor(arg1, arg2);
                }
            }
        ```
    - 执行结果：
        ```java
            外层-第一个  -  内层-第一个
            外层-第一个  -  内层-第二个
            外层-第一个  -  内层-第三个
            外层-第二个  -  内层-第一个
            外层-第二个  -  内层-第二个
            外层-第二个  -  内层-第三个
            外层-第三个  -  内层-第一个
            外层-第三个  -  内层-第二个
            外层-第三个  -  内层-第三个
        ```
- 直角三角形（左）：
    - 说明：
        - 打印出直角三角形，居左展示。
    - 代码：
        ```java
            package com.tsing.algorithm.dichotomysearch;

            public class LeftTriangle {
                
                public static int[] leftTriangle() {
                    int n = 10;
                    
                    for (int i = 0; i < n; i++) {
                        for (int j = 0; j <= i; j++) {
                            System.out.print("* ");
                        }
                        System.out.println();
                    }
                    return null;
                }
                
                public static void main(String[] args) {
                    leftTriangle();
                };
            }
        ```
    - 执行结果：
        ```java
            * 
            * * 
            * * * 
            * * * * 
            * * * * * 
            * * * * * * 
            * * * * * * * 
            * * * * * * * * 
            * * * * * * * * * 
            * * * * * * * * * * 
        ```
- 直角三角形（右）：
    - 说明：
        - 打印出直角三角形，据右展示。
    - 代码：
        ```java
            package com.tsing.algorithm.dichotomysearch;

            public class RightTriangle {
                
                public static int[] rightTriangle() {
                    int n = 10;
                    
                    for (int i = 1; i <= n; i++) {
                        for (int k = 1; k <= n - i; k++) {
                            System.out.print(" ");
                        }
                        for (int j = 1; j <= i; j++) {
                            System.out.print("*");
                        }
                        System.out.println();
                    }
                    return null;
                }
                
                public static void main(String[] args) {
                    rightTriangle();
                };
            }
        ```
    - 执行结果：
        ```java
                    *
                   **
                  ***
                 ****
                *****
               ******
              *******
             ********
            *********
           **********
        ```