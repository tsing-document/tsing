#### 运算符

- 概要：
    - 算符运算符：
        - 分类：
            - `-` `+` `*` `/` `%` `--` `++`
    - 赋值运算符：
        - 分类：
            - `=`
    - 比较运算符：
        - 分类：
            - `>` `>=` `<` `<=` `==` `!=`
    - 逻辑运算符：
        - 分类：
            - `&&` `&` `||` `|` `!` `^`
    - 位运算符：
- 语法：
- 案例：
    ```java
        //算符运算符：
            int a = 7;
            int b = 2;

            //加法
            System.out.println(a + b);

            //减法
            System.out.println(a - b);

            //乘法
            System.out.println(a * b);

            //除法 这个是获取的整数
            System.out.println(a / b);

            //求余
            System.out.println(a % b);

            //-- 放在左边先进行运算再执行 -- 操作，放在右边先执行 -- 再进行运算
            System.out.println(a--);

            //++ 放在左边先进行运算再执行 ++ 操作，放在右边先执行 ++ 再进行运算
            System.out.println(a++);

            //输出结果：9
            //System.out.println(a++ + b);

            //输出结果：10
            //System.out.println(++a + b);

            //输出结果：5
            //System.out.println(a-- -b);

            //输出结果：4
            System.out.println(--a -b);
        //赋值运算符：
            String a = "测试";

        //比较运算符：
            int a = 5;
            int b = 10;

            //大于
            System.out.println(a > b);

            //大于等于
            System.out.println(a >= b);

            //小于
            System.out.println(a < b);

            //小于等于
            System.out.println(a <= b);

            //等于
            System.out.println(a == b);

            //不等于
            System.out.println(a != b);

            //对象比较的是地址
            Comparable c1 = new Comparable();
            Comparable c2 = new Comparable();
            System.out.println(c1 == c2);

            System.out.println(c1 != c2);
        //逻辑运算符：
            boolean a = true;
            boolean b = false;

            //与，前后两个操作数必须都是true才是true,否则返回false
            System.out.println(a && b); //false

            //不断路与，和与相同，只是表达式两边都要算出结果才会执行
            System.out.println(a & b);  //false

            //或，只要表达式两边有一个为 true 就返回true,否则返回false。
            System.out.println(a || b); //true

            //短路或，和或相同，只是表达式两边都要算出结果才会执行
            System.out.println(a | b);  //true

            //非，只需要一个操作数，如果操作数返回true,结果就会为false,反之就是true
            System.out.println(!a); //false
            System.out.println(!b); //true

            //异或，当两个操作数不同时才会返回true,当两个操作数相同则返回false
            System.out.println(true ^ true); //false
            System.out.println(true ^ false); //true
            System.out.println(false ^ true); //true
            System.out.println(false ^ false); //false



    ```
