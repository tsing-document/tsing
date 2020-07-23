# 双重 for 循环打印出你想要的任何形状
- hello world：
    - 说明：
        - 直观的看出双重 `for` 执行策略
    - 示例：
        ```java
            package com.tsing.algorithm.dichotomysearch;

            public class DoubleFor {
                
                public static int[] towSum (String[] arg1,String[] arg2) {
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
                    towSum(arg1, arg2);
                }
            }
        ```
    - 执行结果：
        ```java
            外层-第一个内层-第一个
            外层-第一个内层-第二个
            外层-第一个内层-第三个
            外层-第二个内层-第一个
            外层-第二个内层-第二个
            外层-第二个内层-第三个
            外层-第三个内层-第一个
            外层-第三个内层-第二个
            外层-第三个内层-第三个
        ```