# 流程控制
- 概念：
    ```java
        //1.if

        //2.if...else

        //3.if...else if...else...
    ```
- 语法：
    ```java
        //1. if
        if(条件表达式){
            //执行代码块
        }

        //2.if...else
        if(条件表达式){
            //条件表达式为真执行的代码块
        } else {
            //条件表达式为假执行的代码块
        }

        //3.if...else if...else...
        if(条件表达式){
            //条件表达式符合条件执行的代码块
        } else if(条件表达式) {
            //条件表达式符合条件执行的代码块
        } else {
            //默认执行的代码块
        }
    ```
- 案例：
    ```java
        public static void main (String[] args) {
            int a = 15;
            //1.if
            if(a<6){
                System.out.println("简单的判断语句");
            }
            //2.if...else...
            if(a<6){
                System.out.println("if...else... 条件表达式为真");
            } else {
                System.out.println("if...else... 条件表达式为假");
            }

            //3.if...else if...else...
            if(a<6){
                System.out.println("if...else if...else... 条件表达式为真");
            } else if(a==6){
                System.out.println("if...else if...else... 条件表达式为假");
            } else {
                System.out.println("默认执行的代码块");
            }
        }
    ```