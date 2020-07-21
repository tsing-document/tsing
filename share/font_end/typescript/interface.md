# 接口
- 接口初探：
    ```js
        function printLable ( labelledObj: { lable : string } ) {
            console.log(labelledObj.lable);
        };

        let myObj = {
            size: 10,
            lable: 'Size 10 Object',
        };

        printLable(myObj);
    ```
- 改造接口：
    ```js
        /* 使用接口声明 */
        interface LabelledValue {
            lable : string;
        }

        function printLable ( labelledObj: LabelledValue ) {
            console.log(labelledObj.lable);
        };

        let myObj = {
            size: 10,
            lable: 'Size 10 Object',
        };

        printLable(myObj);
    ```
- 可选属性：
    ```css
        /* 这个代码 myObj 会报错 */
        interface LabelledValue {
            lable: string;
            color: string;
        }

        function printLable ( labelledObj: LabelledValue ) {
            console.log(labelledObj.lable);
            console.log(labelledObj.color);
        };

        let myObj = {
            size: 10,
            lable: 'Size 10 Object',
        };

        printLable(myObj);

        /* 这样就不会报错了 */
        interface LabelledValue {
            lable: string;
            color?: string; //因为这个地方加了 ？
        }

        function printLable ( labelledObj: LabelledValue ) {
            console.log(labelledObj.lable);
            console.log(labelledObj.color);
        };

        let myObj = {
            size: 10,
            lable: 'Size 10 Object',
        };

        printLable(myObj);
    ```
- 只读属性：
    ```css
        /* 
            一些对象属性只能在对象刚刚创建的时候修改其值。可以在属性名前用 readonly 来指定只读属性
            赋值之后就不能改变了。
        */
        interface LabelledValue {
            readonly lable: string;
            readonly color: string;
        }

        function printLable ( labelledObj: LabelledValue ) {
            console.log(labelledObj.lable);
            console.log(labelledObj.color);
        };

        let myObj: LabelledValue = {
            color: 'red',
            lable: 'Size 10 Object',
        };

        // myObj.lable = 'dee'; //报错

        printLable(myObj as LabelledValue); // as LabelledValue 是断言
    ```

- 类类型：
    - 实现接口：
        - 