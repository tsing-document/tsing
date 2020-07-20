# width宽度、 height高度
- 概要：
    - height
    - max-height
    - min-height
    - width
    - max-width
    - min-width
- 语法：
    ```css
        /* 1.设置对象的高度 */
        height

        /* 2.设置目标的最大高度 */
        max-height

        /* 3.设置目标的最小高度 */
        min-height

        /* 4.设置对象的宽度 */
        width

        /* 5.设置目标的最大宽度 */
        max-width

        /* 6.设置目标的最小宽度 */
        min-width
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>width宽度、height高度</title>
            <style type="text/css">
            </style>
        </head>
        <body>
            <!--
                1.设置对象的高度
                    - height
            -->
            <h2>height</h2>
            <div style="height: 100px;background-color: red;">
                测试文字
            </div>

            <!--
                2.设置目标的最大高度
                    - max-height
            -->
            <h2>max-height</h2>
            <div style="background-color: red; max-height: 200px;">
                测试文字
            </div>

            <!--
                3.设置目标的最小高度
                    - min-height
            -->
            <h2>min-height</h2>
            <div style="background-color: red; min-height: 160px;">
                测试文字
            </div>

            <!--
                4.设置对象的宽度
                    - width
            -->
            <h2>width</h2>
            <div style="background-color: red;width: 500px;">
                测试文字
            </div>

            <!--
                5.设置目标的最大宽度
                    - max-width
            -->
            <h2>max-width</h2>
            <div style="background-color: red;max-width: 400px;">
                测试文字
            </div>

            <!--
                6.设置目标的最小宽度
                    - min-width
            -->
            <h2>min-width</h2>
            <div style="background-color: red;min-width: 1200px;">
                测试文字
            </div>
        </body>
        </html>
    ```
