# box-sizing css3 新增
- 概要：
    - content-box
    - border-box
    - inherit
- 语法：
    ```css
        /* 1.控制元素的内容区域的高度和宽度 */
        content-box

        /* 2.控制元素的内容区域加内填充再加边框区的宽度和高度 */
        border-box

        /* 3.从父元素继承 box-sizing 属性的值 */
        inherit
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>大小相关属性</title>
            <style type="text/css">
            </style>
        </head>
        <body>
            <h2>原始</h2>
            <div style="width: 200px;
                        height: 40px;
                        background-color: #ddd;
                        background-clip: content-box;">
                测试文字
            </div>

            <h2>增加border和padding区</h2>
            <div style="width: 200px;
                        height: 40px;
                        background-color: #ddd;
                        border: 30px solid #555;
                        padding: 30px;">
                测试文字
            </div>

            <h2>box-sizing属性 - content-box</h2>
            <div style="width: 200px;
                        height: 100px;
                        background-color: #ddd;
                        background-clip: content-box;
                        border: 20px solid #555;
                        padding: 20px;
                        box-sizing: content-box;">
                测试文字
            </div>

            <h2>box-sizing属性 - border-box</h2>
            <div style="width: 200px;
                        height: 100px;
                        background-color: #ddd;
                        background-clip: content-box;
                        border: 20px solid #555;
                        padding: 20px;
                        box-sizing: border-box;">
                测试文字
            </div>
        </body>
        </html>
    ```
