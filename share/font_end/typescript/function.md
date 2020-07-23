# 函数

- 招式一：函数声明
    ```ts
        function sum(x: number, y:number): number {
            return x + y;
        };
        
        console.log(sum(1, 3)); //correct

        /*
            1.参数的个数是不能修改的。
        */
        console.log(sum(1, 3, 4)); //error: Expected 2 arguments, but got 3
        console.log(sum(1)); //error: Expected 2 arguments, but got 1
    ```
- 招式二：函数表达式
    ```ts
        /*
            = 右边是函数表达式，左边可以添加输入类型的定义
        */
        const sum3 = function (x: number, y: number): number {
            return x + y;
        };

        console.log(sum3(2,3));


        /*
            = 左边多了 : (x: number, y: number) => number，这个 => 不是我们熟悉的 ES6 箭头函数中的 =>。 Ts 中的 => 是用来定义函数的，函数左边是输入类型（用()括号括起来），右侧是输出类型。其实多出来的内容也可以不用手动添加，因为通过赋值操作也可以将类型推论出来。
        */
        const sum4: (x: number, y: number) => number = function (x: number, y:number): number {
            return x + y;
        }

        console.log(sum4(3,7));
    ```
- 招式三：接口定义

- 可选参数：
    ```ts
        /*
            可选参数后面不能再加参数。
        */
        const sum3 = function (x: number, y: number, z?: number): number {
            return x + y;
        };

        console.log(sum3(2,3));
    ```
- 剩余参数：
    ```ts
        const push = (array: any[], ...rest: any[]) => {
            rest.forEach(r => {
                array.push(r);
            });
        };

        let arr = [false];
        push(arr, '1', 2, 3);

        /*
            error
                参数 array 和 ...rest 我们定义了类型， ...rest 其实就是一个数组。
                另外，剩余参数和可选参数后面都不能有参数。
        */
        const push1 = (array: any[], ...rest: any[], x: number) => {
            rest.forEach(r => {
                array.push(r);
            });
            rest.push(x);
        };
    ```
- 默认值：
    ```ts
            const demo1 = (firstName: string = 'pr', lastName?: string, ...rest: any[]): string => {
            let tmp: string = '';
            if(rest.length) {
                tmp = rest.join(' ');
            }
            if(lastName) {
                return `${firstName}-${lastName}-${tmp}-`;
            } else {
                return `${firstName}+${tmp}`;
            }
        };

        console.log(demo1());
        console.log(demo1('青衣', '男', '今年', 25));
    ```
- 重载：
    

