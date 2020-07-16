# 背景
- 概要：
    ```css
        background:
            - background-color
            - background-image
            - background-repeat
            - background-attachment
            - background-position
        background-color
        background-image
        background-repeat
        background-attachment
            - scroll(背景不固定)
            - fixed(背景固定)
        background-position
    ```
- 语法：
    ```css
        /*
            1.设置背景色。如果同时设置背景色和背景图片，则背景图片将覆盖背景色。
        */
        background-color

        /*
            2.设置背景图片。如果同时设置了背景色和背景图片，则背景图片覆盖背景颜色。
        */
        background-image
        
        /*
            3.适用于 css1。用于设置背景图片是否平铺。
            在指定该属性之前，必须先指定 background-image 属性。
            该属性有 repeat、no-repeat、repeat-x、repeat-y
        */
        background-repeat
            - repeat
                - 纵向和横向同时平铺
            - no-repeat
                - 不平铺
            - repeat-x
                - 仅在横向平铺
            - repeat-y
                - 仅在纵向平铺

        /*
            4.设置背景图片是随对象内容滚动还是固定。
              在指定该属性之前，必须先指定 background-image 属性。
        */
        background-attachment
            - scroll(背景不固定) 默认值
            - fixed(背景固定)

        /*
            5.设置背景图片的位置，该属性需要横坐标和纵坐标两个值。
            在指定该属性之前，必须先指定 background-image 属性。
        */
        background-position

        /* 
            6.设置对象背景样式。该属性是一个复合属性，可用于控制
                背景颜色、
                背景图片、
                背景重复模式
            等属性。
            下列是可选值
        */
        background:
            - background-color
            - background-image
            - background-repeat
            - background-attachment
            - background-position
        
    ```
- 案例：
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 背景相关属性 </title>
            <style type="text/css">
                /* 为 div 元素增加边框 */
                div {
                    border: 1px solid #000000;
                    height: 300px;
                    width: 100%;
                }
                /*
                    background:
                        - background-color
                        - background-image
                        - background-repeat
                        - background-attachment
                        - background-position
                */
            </style>
        </head>
        <body>
            <!--
                1.设置背景色。如果同时设置背景色和背景图片，则背景图片将覆盖背景色。
                    background-color
            -->
            <div style="background-color: chartreuse;">
                测试文字
            </div>

            <!--
                2.设置背景图片。如果同时设置了背景色和背景图片，则背景图片覆盖背景颜色。
                    background-image
            -->
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);">
                测试文字
            </div>

            <!--
                3.适用于 css1。用于设置背景图片是否平铺。
                    在指定该属性之前，必须先指定 background-image 属性。
                    该属性
                    background-repeat
            -->
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);background-repeat: no-repeat;">
                测试文字
            </div>
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);background-repeat: repeat-x;">
                测试文字
            </div>
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);background-repeat: repeat-y;">
                测试文字
            </div>

            <!--
                4.设置背景图片是随对象内容滚动还是固定。
                    在指定该属性之前，必须先指定 background-image 属性。
                    background-attachment
                        - scroll(背景不固定)
                        - fixed(背景固定)
            -->
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);background-attachment:fixed;width: 100%;height: 1000px;;">
                测试文字
            </div>

            <!--
                5.设置背景图片的位置，该属性需要横坐标和纵坐标两个值。
                    在指定该属性之前，必须先指定 background-image 属性。
                        background-position
            -->
            <div style="background-image: url(http://img4.imgtn.bdimg.com/it/u=3318627154,792532200&fm=214&gp=0.jpg);background-repeat:no-repeat;background-position:100px 200px">
                测试文字
            </div>
        </body>
        </html>
    ```