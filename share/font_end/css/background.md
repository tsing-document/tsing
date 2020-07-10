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

        /*
           css3 新增
        */
        background-clip
        background-origin
        background-size
        border-box
        no-clip
        padding-box
        content-box

        background-origin
            - border-box
            - padding-box
            - content-box
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
            /*
                    background:
                        - background-image
                        - background-repeat
                        - background-attachment
                        - background-position
            */
            div {
                border: 1px solid black;
                height: 500px;
                width: 1000px;
                text-align: center;
            }

            </style>
        </head>
        <body>
            <!-- background-color -->
            <h2>灰色背景</h2>
            <div style="background-color: #aaa;">
                测试文字
            </div>
            
            <!--
                background-image
                background-repeat
                background-position
                background-image
            -->
            <h2>背景图片</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594362602262&di=a1067d79275a56e2330bccf484c210f2&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201810%2F27%2F20181027080835_epxxl.thumb.700_0.jpeg);" >
                测试文字
            </div>

            <h2>不平铺的背景图片</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594361073487&di=d48a3a4ac875a17b7a4d6e12c20f39a1&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F52%2F52%2F01200000169026136208529565374.jpg);background-repeat: no-repeat;" >
                测试文字
            </div>
            
            <h2>仅横向平铺的背景图片</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594361073487&di=d48a3a4ac875a17b7a4d6e12c20f39a1&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F52%2F52%2F01200000169026136208529565374.jpg);background-repeat: repeat-x;" >
                测试文字
            </div>

            <h2>不平铺的背景图片，并指定背景图片位置</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594361073487&di=d48a3a4ac875a17b7a4d6e12c20f39a1&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F52%2F52%2F01200000169026136208529565374.jpg);background-repeat: no-repeat;background-position: 35% 80%;" >
                测试文字
            </div>

            <h2>不平铺的背景图片，并指定背景图片位置</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594361073487&di=d48a3a4ac875a17b7a4d6e12c20f39a1&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F52%2F52%2F01200000169026136208529565374.jpg);background-repeat: no-repeat;background-position: 30px 12px;" >
                测试文字
            </div>

            <h2>不平铺的背景图片，并指定背景图片位置</h2>
            <div style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594361073487&di=d48a3a4ac875a17b7a4d6e12c20f39a1&imgtype=0&src=http%3A%2F%2Fa4.att.hudong.com%2F52%2F52%2F01200000169026136208529565374.jpg);background-repeat: no-repeat;background-position: center bottom;" >
                测试文字
            </div>
        </body>
        </html>
    ```
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 背景固定 </title>
            <style type="text/css">

            </style>
        </head>
        <body style="background-image: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1594372822550&di=d06a3c6db8528e601e36bb25d6175b42&imgtype=0&src=http%3A%2F%2Fb-ssl.duitang.com%2Fuploads%2Fitem%2F201805%2F18%2F20180518134730_vnJXa.thumb.700_0.jpeg);background-attachment: fixed;">
            <ul style="font-size: 30pt;">
                <script type="text/javascript">
                    for(var i=0; i < 45; i++) {
                        document.writeln("<li>企业javaee实战</li>");
                    }
                </script>
            </ul>
        </body>
        </html>

    ```
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 背景相关属性 </title>
            <style type="text/css">
                /*
                    background-clip
                    background-origin
                    background-size
                    border-box
                    no-clip
                    padding-box
                    content-box
                */

                div {
                    border: 10px solid #444;
                    padding: 12px;
                    height: 800px;
                    width: 1800px;
                }
            </style>
        </head>
        <body>
            <h2>设置背景覆盖的范围</h2>
            <div style="background-image: url(https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1829417806,1400660466&fm=26&gp=0.jpg);">
                测试文字
            </div>

            <h2>设置背景覆盖的范围</h2>
            <div style="background-image: url(https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1829417806,1400660466&fm=26&gp=0.jpg);background-clip: no-clip;">
                测试文字
            </div>

            <h2>设置背景覆盖的范围</h2>
            <div style="background-image: url(https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1829417806,1400660466&fm=26&gp=0.jpg);background-clip: padding-box;">
                测试文字
            </div>

            <h2>设置背景覆盖的范围</h2>
            <div style="background-image: url(https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=1829417806,1400660466&fm=26&gp=0.jpg);background-clip: content-box;">
                测试文字
            </div>
        </body>
        </html>
    ```










            background:
            - 设置对象的背景样式。该属性是一个复合属性，可用于同时设置背景色、背景图片、背景重复模式等属性。
                ```css
                    background-color
                    background-image
                    background-repeat
                    background-attachment
                    background-position
                ```
        background-color:
            - 设置背景颜色。如果同时设置了背景色和背景图片，则背景图片将覆盖背景色。
        background-image:
            - 用于设置背景图片。如果同时设置了背景色和背景图片，则背景图拍呢将覆盖背景颜色。该属性需要使用 `url()` 函数指定图片地址，图片地址既可以是相对位置，也可以是绝对地址。
        background-repeat:
            - 适用于css1, 用于设置对象的背景图片是否平铺。在指定该属性之前，必须先指定background-image属性。该属性有 `repeat`、`no-repeat`、`repeat-x`、`repeat-y`这四个值。分别对应在纵向和横向同时平铺、不平衡、仅在横向平铺、仅在纵向平铺。
        background-attachment:
            - 用于设置图片背景图片是随对象内容滚动还是固定。在指定该属性之前，必须先指定 backgroun-image 属性，该属性支持下面两个值：
                - scroll
                - fixed
        background-position:
            - 对象背景图片的位置。


             background:
            - 设置对象的背景样式。该属性是一个复合属性，可用于同时设置背景色、背景图片、背景重复模式等属性。
                ```css
                    background-color
                    background-image
                    background-repeat
                    background-attachment
                    background-position
                ```
        background-color:
            - 设置背景颜色。如果同时设置了背景色和背景图片，则背景图片将覆盖背景色。
        background-image:
            - 用于设置背景图片。如果同时设置了背景色和背景图片，则背景图拍呢将覆盖背景颜色。该属性需要使用 `url()` 函数指定图片地址，图片地址既可以是相对位置，也可以是绝对地址。
        background-repeat:
            - 适用于css1, 用于设置对象的背景图片是否平铺。在指定该属性之前，必须先指定background-image属性。该属性有 `repeat`、`no-repeat`、`repeat-x`、`repeat-y`这四个值。分别对应在纵向和横向同时平铺、不平衡、仅在横向平铺、仅在纵向平铺。
        background-attachment:
            - 用于设置图片背景图片是随对象内容滚动还是固定。在指定该属性之前，必须先指定 backgroun-image 属性，该属性支持下面两个值：
                - scroll
                - fixed
        background-position:
            - 对象背景图片的位置。