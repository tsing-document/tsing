# 基础类型

- 布尔值（`boolean`）：
    ```js
        let isDone: boolean = false;
    ```
- 数字（`number`）：
    ```js
        /*
            所有的数字都是浮点数。
        */
        let decLiteral: number = 6;
        let hexLiteral: number = 0xf00d;
        let binaryLiteral: number = 0b1010;
        let octalLiteral: number = 0o744;
    ```
- 字符串（`string`）：
    ```js
        /*
            基本使用
        */
        let name: string = "bob";
        name = "smith";

        /*
            模版字符串，内嵌表达式。
        */
        let name: string = `Gene`;
        let age: number = 37;
        let sentence: string = `Hello, my name is ${ name }`,
                                I'll be ${ age +1 } years old next month.`;

    ```
- 数组（`arr`）：
    ```js
        /*
            第一种定义方式
        */
        let list: number[] = [1, 2, 3];

        /*
            第二种定义方式
        */
        let list Array<number> = [1, 2, 3];
    ```
- 元组（`Tuple`）：
    ```js
        /*
            元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。
        */
        let x: [string, number];

        x = ['hello', 10];

        console.log(x[0]);
        console.log(x[1]);
    ```
- 枚举（`enum`）：
    ```js
        enum Color { Red = 1, Green = 2, Blue = 4};
        let colorName: string = Color[1];
        let c: Color = Color.Green;

        console.log(colorName);
        console.log(c);
    ```
- Any：
    ```js
        /*
            any 就和 java 中的 object 类型一样
        */
        const a: any = 10;
        const b: any = 'hello';
        const c: any = [1, 2, 3];

        console.log(a);
        console.log(b);
        console.log(c);
    ```
- Void：
    ```js
        /*
            当一个函数没有任何返回值时，会用到 void
        */
        function demofunction(): void {
            console.log('test');
        };

        function demofunction1(): any {
            return '有返回值';
        };

        demofunction();

        console.log(demofunction1());
    ```
- Null和Undefined：
- Never：
- object：
- 类型断言：
    ```js
        /*
            类型断言只会在编译阶段起作用。
        */

        /* 第一种 */
        let someValue: any = "this is a string";

        let strLength: number = (<string>someValue).length;

        /* 第二种 */
        let someValue: any = "this is a string";

        let strLength: number = (someValue as string).length;
    ```