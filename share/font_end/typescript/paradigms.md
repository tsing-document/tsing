# 范型

- hello world：
    ```ts
        // 定义函数
        function identity<T>(arg: T): T {
            return arg;
        };

        // 调用函数
        let output = identity<string>('测试');
        console.log(output);
    ```
- 使用范型变量：
    ```ts
        function identity<T>(arg: T[]): number {
            return arg.length;
        };

        const arr = ['测试1','测试2'];

        let output = identity<string>(arr);
        console.log(output);
    ```
- 范型类型：
    