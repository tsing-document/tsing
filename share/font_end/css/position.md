# 定位
- 概要：
    - position
        - absolute
        - relative
        - static
    - z-index
    - top
    - right
    - bottom
    - left
- 语法：
    ```css
        /* 1.设置目标的定位方式,下面是可选项 */
        position
            - absolute /* 允许将该对象漂浮在页面之上 */
            - relative /* 元素参照前一个对象的位置进行定位 */
            - static   /* 以页面为参照物 */

        /* 2.设置对象的漂浮层的等级，该值越大，漂浮层越漂浮在上面 */
        z-index

        /* 
            3.用于设置目标对象相对于最近一个具有定位设置的父对象的顶边偏移，此属性仅当
              对象的 position 属性为 absolute、relative时有效。
        */
        top

        /*
            4.设置目标对象相对于最近一个具有定位设置父对象的右边偏移，此属性仅当
              对象的 position 属性为 absolute、relative时有效。
        */
        right

        /*
            5.设置目标对象相对于最近一个具有定位设置父对象的底边偏移，此属性仅当
              对象的 position 属性为 absolute、relative时有效。
        */
        bottom

        /*
            6.设置目标对象相对于最近一个具有定位设置的父对象的左边偏移，此属性仅当
              对象的 position 属性为 absolute、relative时有效。
        */
        left
    ```
- 案例：
    ```css
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>定位</title>
            <style type="text/css">
            </style>
        </head>
        <body>
            html5<br/>
            ldiogn<br/>
            ldiogn<br/>
            ldiogn<br/>
            ldiogn<br/>
            ldiogn<br/>
            ldiogn<br/>
            ldiogn<br/>
            <div
                id="layer1"
                style="position: absolute;
                    left: 40px;
                    top: 20px;
                    width: 190px;
                    height: 100px;
                    z-index: 2;
                    background-color: #ccc;">
                layer1 使用 position 属性值为 absolute, 该元素完全漂浮在页面之上，不受其他对象的位置影响。z-index:2
            </div>

            <div id="layer2"
                style="position: relative;
                    left: 50px;
                    top: 10px;
                    width: 200px;
                    height: 100px;
                    z-index: 3;
                    background-color: #999;">
                layer2, 使用 position 属性值为 relative，该元素将漂浮在页面之上，但他将基于上面最后一行文本进行定位。z-index:3
            </div>

            <div style="position: absolute;
                        left: 260px;
                        top: 80px;
                        width: 250px;
                        height: 200px;
                        border: 2px solid black;">
                <div id="layer3"
                    style="position: static;
                            left: 100px;
                            top: 40px;
                            width: 80px;
                            height: 88px;
                            z-index: 1;
                            background-color: #666;">
                    position: static
                </div>

                <div id="layer4"
                    style="position: static;
                            left: 100px;
                            top: 80px;
                            width: 80px;
                            height: 88px;
                            z-index: 1;
                            background-color: #999;">
                    position: static
                </div>
            </div>
        </body>
        </html>
    ```