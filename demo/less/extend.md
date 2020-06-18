# 扩展
- 扩展语法：
    - 概念：
        - extend 可以附加给一个选择器，也可以放入一个规则集中。它看起来像一个带选择器参数伪类，也可以用关键字 `all` 选择相邻的选择器。
        ```html
            <div>
                <div class='a'>
                    函数
                </div>
            </div>
        ```
        ```less
            .b {
                background-color: blue;
            }

            .a:extend(.b){}
        ```