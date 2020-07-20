# 轮廓
- 概要：
    - outline-color
    - outline-style
        - none
        - dotted
        - dashed
        - solid
        - double
        - groove
        - ridge
        - inset
        - outset
    - outline-width
    - outline-offset
    - outline
- 语法：
    ```css
        /* 1.设置元素的轮廓颜色 */
        outline-color

        /* 2.设置元素的轮廓线型，下面是可选项 */
        outline-style
            - none
            - dotted
            - dashed
            - solid
            - double
            - groove
            - ridge
            - inset
            - outset
        
        /* 3.设置目标元素的轮廓宽度 */
        outline-width

        /* 4.设置目标元素的罗扩偏移距离 */
        outline-offset

        /* 5.这是一个复合属性 */
        outline
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>轮廓</title>
            <style type="text/css">
                body {
                    font-size: 16pt;
                }

                div {
                    font-size: 12pt;
                    width: 400px;
                    height: 60px;
                    border: 1px solid black;
                }
            </style>
        </head>
        <body>
            <h2>outline-demo1</h2>
            <div style="outline: rgba(50, 50, 50, 0.5) solid 10px">
                测试文字
            </div>

            <h2>outline-demo2</h2>
            <div style="outline: rgba(50, 50, 50, 0.5) dotted 10px">
                测试文字
            </div>

            <h2>outline-demo2</h2>
            <div style="outline: rgba(50, 50, 50, 0.5) dotted 10px;outline-offset:10px">
                测试文字
            </div>
        </body>
        </html>
    ```
