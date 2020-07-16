# css3 新增背景相关
- 概要：
    - css3 新增背景相关的属性
        - background-clip
        - background-origin
        - background-size
        - border-box
        - no-clip
        - padding-box
        - content-box
        - background-repeat
- 语法：
    ```css
        /* css3 新增背景相关的属性 */
            /*
                1.设置背景覆盖的范围。
            */
            background-clip
                - border-box /* 背景覆盖和模型的边框区、内填充区、内容区域。 */
                - no-clip /* 背景覆盖和模型的边框区、内填充区、内容区域。 */
                - padding-box /* 背景覆盖盒模型的内填充区、内容区。 */
                - content-box /* 指定背景只覆盖盒模型的内容区。*/
            /*
                2.设置背景覆盖的起点。
            */
            background-origin
                - padding-box
                - border-box
                - content-box

            /*
                3.设置背景图片的大小。
            */
            background-size
            
            /*
                4.
            */
            background-repeat
                - space
                - round
    ```
- 案例：
    - css3 新增背景相关的属性：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title> css3 新增背景相关的属性 </title>
                <style type="text/css">
                    /* 为 div 元素增加边框 */
                    div {
                        border: 10px dotted #000000;
                        padding: 50px;
                        margin: 30px;
                        height: 60px;
                        width: 100%;
                    }
                    /*
                        - background-clip
                        - background-origin
                        - background-size
                        - border-box
                        - no-clip
                        - padding-box
                        - content-box
                    */

                    #morepic {
                        border: 1px solid #000;
                        height: 400px;
                        width: 100%;

                        background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594890283224&di=5be84a4abbcefa58342d94385f7c4a4d&imgtype=0&src=http%3A%2F%2Fa3.att.hudong.com%2F00%2F38%2F01300000241358127660380294217.jpg),
                                        url(https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1320272459,772040234&fm=26&gp=0.jpg),
                                        url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2481321790,3127612340&fm=26&gp=0.jpg);
                        background-repeat: repeat-y, repeat-x ,repeat;

                        background-position: center top, left center, left top;
                    }
                </style>
            </head>
            <body>
                <!--
                    1.设置背景覆盖的范围。
                        - background-clip
                            - border-box /* 背景覆盖和模型的边框区、内填充区、内容区域。 */
                            - no-clip /* 背景覆盖和模型的边框区、内填充区、内容区域。 */
                            - padding-box /* 背景覆盖盒模型的内填充区、内容区。 */
                            - content-box /* 指定背景只覆盖盒模型的内容区。*/
                -->
                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg)">
                    background-clip 默认
                </div>

                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-clip:content-box">
                    background-clip: content-box
                </div>

                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-clip:padding-box">
                    background-clip: padding-box
                </div>

                <!--
                    2.设置背景覆盖的起点。
                        background-origin
                            - padding-box
                            - border-box
                            - content-box
                -->
                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-origin: content-box">
                    background-clip: padding-box
                </div>

                <!--
                    3.设置背景图片的大小。
                        - background-size
                -->
                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-size: 90px">
                    background-size
                </div>

                <!--
                    4.
                        - background-repeat
                -->
                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-repeat:round">
                    background-repeat: round
                </div>
                <div style="background-image: url(https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1091579268,2185400060&fm=26&gp=0.jpg);
                                                background-repeat:space">
                    background-repeat: space
                </div>


                <!--
                    5.指定多张图片
                -->
                <div id="morepic"></div>
            </body>
            </html>
        ```