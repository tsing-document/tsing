# resize css3新增
- 概要：
    - resize
        - none
        - both
        - horizontal
        - vertical
        - inherit
- 语法：
    ```css
        /*
            对所有设置了 overflow 的 html 元素有效
        */

        /* 1.不允许用户通过拖动来改变元素的大小 */
        none

        /* 2.不允许用户通过拖动来改变元素的高度和宽度 */
        both

        /* 3.不允许用户通过拖动来改变元素的宽度 */
        horizontal

        /* 4.不允许用户通过拖动高度 */
        vertical

        /* 5.继承自父元素的resize属性值，这是默认值 */
        inherit
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>resize属性</title>
            <style type="text/css">
            </style>
        </head>
        <body>
            <h2>none</h2>
            <div style="width: 200px;
                        height: 40px;
                        background-color: #ddd;
                        border: 2px solid black;
                        resize: none;
                        overflow: auto;">
                测试文字
            </div>

            <h2>both</h2>
            <div style="width: 200px;
                height: 40px;
                background-color: #ddd;
                border: 2px solid black;
                resize: both;
                overflow: auto;">
                测试文字
            </div>

            <h2>horizontal</h2>
            <div style="width: 200px;
                height: 40px;
                background-color: #ddd;
                border: 2px solid black;
                resize: horizontal;
                overflow: auto;">
                测试文字
            </div>

            <h2>vertical</h2>
            <div style="width: 200px;
                height: 40px;
                background-color: #ddd;
                border: 2px solid black;
                resize: vertical;
                overflow: auto;">
                测试文字
            </div>

            <h2>inherit</h2>
            <div style="width: 200px;
                height: 40px;
                background-color: #ddd;
                border: 2px solid black;
                resize: vertical;
                overflow: auto;">
                    外部测试
                    <div style="width: 200px;
                        height: 40px;
                        background-color: red;
                        border: 2px solid black;
                        resize: inherit;
                        overflow: auto;">
                             内部测试
                    </div>
            </div>
        </body>
        </html>
    ```
