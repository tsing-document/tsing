# 边框相关的属性
- 概要：
    - border-color
    - border-style
    - border-width
    - border-top
    - border-top-color
    - border-top-style
    - boder-top-width
    - boder-right
    - border-right-color
    - border-right-style
    - border-right-width
    - border-bottom
    - border-bottom-color
    - border-bottom-style
    - border-bottom-width
    - border-left
    - border-left-color
    - border-left-style
    - border-left-width
    - 边框的线型：
        - none
        - hidden
        - dotted
        - dashed
        - solid
        - double
        - groove
        - ridge
        - inset
        - outset
- 语法：
    ```css
        /* 1.边框颜色 */
        border-color

        /* 2.设置元素的边框线型 */
        border-style

        /* 3.设置边框线宽 */
        border-width

        /* 4.这是复合属性，设置元素的上边框样式 可同时设置边框的粗细、线型、颜色。 */
        border-top

        /* 5.设置上边框的颜色 */
        border-top-color

        /* 6.设置上边框的线型 */
        border-top-style

        /* 7.设置上边框的宽度 */
        border-top-width

        /* 8.这是复合属性，设置元素的右边框的粗细、线型、颜色 */
        border-right

        /* 9.设置右边框的颜色 */
        border-right-color

        /* 10.设置右边框的线型 */
        border-right-style

        /* 11.设置右侧边框的宽度 */
        border-right-width

        /* 12.这个复合属性，设置元素的底边框的粗细、线型、颜色。 */
        border-bottom

        /* 13.设置底部边框的颜色 */
        border-bottom-color

        /* 14.设置底部边框的线型 */
        border-bottom-style

        /* 15.设置底部边框的宽度 */
        border-bottom-width

        /* 16.这个复合属性，设置元素的左边框的粗细、线型、颜色。 */
        border-left

        /* 17.设置左边框的颜色 */
        border-left-color

        /* 18.设置左边框的线型 */
        border-left-style

        /* 19.设置左边框的宽度 */
        border-left-width

        - 边框的线型：
            - none
            - hidden
            - dotted
            - dashed
            - solid
            - double
            - groove
            - ridge
            - inset
            - outset
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 边框属性 </title>
            <style type="text/css">
            </style>
        </head>
        <body>
            <!--
                1.边框颜色
                    - border-color
            -->
            <h3>border-color</h3>
            <div style="border-color: green;
                        border-style: dotted;">
                测试文字
            </div>

            <!--
                2.设置元素的边框线型
                    - border-style
            -->
            <h3>border-style</h3>
            <div style="border-style: dotted;
                        border-color: red">
                测试文字
            </div>

            <!--
                3.设置边框线宽
                    - border-width 
            -->
            <h3>border-width</h3>
            <div style="border-width: 10px;
                        border-style: dotted;
                        border-color: blue;">
                测试文字
            </div>

            <!--
                4.这是复合属性，设置元素的上边框样式 可同时设置边框的粗细、线型、颜色。
                    - border-top
                8.这是复合属性，设置元素的右边框的粗细、线型、颜色
                    - border-right
                12.这个复合属性，设置元素的底边框的粗细、线型、颜色。
                    - border-bottom
                16.这个复合属性，设置元素的左边框的粗细、线型、颜色。
                    - border-left
            -->
            <h3>border-top</h3>
            <div style="border-top: 2px solid black">
                测试文字
            </div>

            <!--
                5.设置上边框的颜色
                    - border-top-color
                9.设置右边框的颜色
                    - border-right-color
                13.设置底部边框的颜色
                    - border-bottom-color
                17.设置左边框的颜色 
                    - border-left-color
                
            -->
            <h3>border-top-color</h3>
            <div style="border-top-color:hotpink;
                        border-top-style: dotted;">
                测试文字
            </div>

            <!--
                6.设置上边框的线型
                    - border-top-style
                10.设置右边框的线型
                    - border-right-style
                14.设置底部边框的线型
                    - border-bottom-style
                18.设置左边框的线型
                    - border-left-style
            -->
            <h3>border-top-style</h3>
            <div style="border-top-style: dotted;
                        border-top-color:hotpink;">
                测试文字
            </div>

            <!--
                7.设置上边框的宽度
                    - boder-top-width
                11.设置右侧边框的宽度
                    - border-right-width
                15.设置底部边框的宽度
                    - border-bottom-width
                19.设置左边框的宽度
                    - border-left-width
            -->
            <h3>boder-top-width</h3>
            <div style="border-top-width: 14px;
                        border-top-style: dotted;
                        border-top-color:hotpink;">
                测试文字
            </div>

        </body>
        </html>
    ```