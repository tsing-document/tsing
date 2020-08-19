# 流程控制
- 概念：
    ```java
        //1.if

        //2.if...else

        //3.if...else if...else...

        //4.switch

        //5.跳出循环体：break和continue
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

        //4.switch
        switch(expression){
            case value :
            //语句
            break; //可选
            case value :
            //语句
            break; //可选
            //你可以有任意数量的case语句
            default : //可选
            //语句
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

            //4.switch
            int a = 10;

            switch(a){
                case 1:
                    System.out.println("得分" + a); 
                break;
                case 2:
                    System.out.println("得分" + a); 
                break;
                case 3:
                    System.out.println("得分" + a); 
                break;
                case 4:
                    System.out.println("得分" + a); 
                break;
                case 5:
                    System.out.println("得分" + a); 
                break;
                case 6:
                    System.out.println("得分" + a); 
                break;
                default:
                    System.out.println("没获取得分"); 
            }
    ```