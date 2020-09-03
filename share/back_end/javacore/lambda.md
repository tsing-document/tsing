# lambda 表达式：todo
- 概念：
    - 定义：
        - `lambda` 表达式，也可以称为闭包，它是推动 java8 发布的最重要的新特性。
        - `lambda` 允许把函数作为一个方法的参数（函数作为参数传递方法中）。
        - 使用 `Lambda` 表达式可以使代码变得更加简洁。
    - 重要特征：
        - 可选类型声明：
            - 不需要声明参数类型，编译器可以统一识别参数值。
        - 可选的参数圆括号：
            - 一个参数无需定义圆括号，但多个参数需要定义圆括号。
        - 可选的打括号：
            - 如果主体包含一个语句，就不需要使用打括号。
        - 可选的返回关键字：
            - 如果主体只有一个表达式返回值则编译器会自动返回值，打括号需要指定表达式返回一个数值。
- 语法：
    ```java
        (paramters) -> expression
        或
        (paramters) -> { statements; }
    ```
- 案例：