# 文本
- 概要：
    - text-indent
    - text-overflow
        - clip
        - ellpsis
    - vertival-align
        - auto
        - baseline
        - sub
        - super
        - top
        - middle
        - bottom
        - length
    - text-align
    - direction
    - white-space
        - normal
        - pre
        - nowrap
        - pre-wrap
        - pre-line
        - inherit
    - word-break
        - normal
        - keep-all
        - break-all
    - word-wrap
        - normal
        - break-word
- 语法：
    ```css
        /* 1.段落文本的缩进，默认值是 0 */
        text-indent

        /* 2.溢出文本的处理方法，下面是可选项 */
        text-overflow
            clip
            ellpsis
        
        /* 3.设置目标元素里内容的垂直对齐方式，通常有顶端，底对不齐方式。底部对齐方式 */
        vertival-align
            auto
            baseline
            sub
            super
            top
            middle
            bottom
            length
        
        /* 4.目标元素中文本的水平对齐方式 */
        text-align

        /* 5.设置文本流入的方向 */
        direction

        /* 6.设置目标元素对文本内容中空白的处理方式 */
        white-space
            normal
            pre
            nowrap
            pre-wrap
            pre-line
            inherit
        
        /* 7.目标元素中文本内容的换行方式 */
        word-break
            normal
            keep-all
            break-all
        
        /* 8.目标元素中文本内容的换行方式 */
        word-wrap
            normal
            break-word
    ```
- 案例：
    ```html
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title> 文本相关属性设置 </title>
                <style type="text/css">
                    /* 为 div 元素增加边框 */
                    div {
                        border: 1px solid #000000;
                        height: 30px;
                        width: 200px;
                    }
                </style>
            </head>
            <body>
                <!--
                    1.段落文本的缩进，默认值是 0
                        - text-indent
                -->
                <div style="text-indent: 30pt">
                    测试文字
                </div>

                <!-- 
                    2.溢出文本的处理方法，下面是可选项
                        - text-overflow
                            - clip
                            - ellpsis
                -->
                <div style="white-space: nowrap;overflow: hidden;text-overflow:clip">
                    测试文字测试文字测试文字测试文字测试文字测试文字
                </div>

                <!--
                    3.设置目标元素里内容的垂直对齐方式，通常有顶端，底对不齐方式。底部对齐方式。
                        - vertival-align
                            - auto
                            - baseline
                            - sub
                            - super
                            - top
                            - middle
                            - bottom
                            - length
                -->
                <div>
                    测试
                        <img style="width: 50px; height: 50px;vertical-align:text-top"  src="http://img3.imgtn.bdimg.com/it/u=2670030773,3413000702&fm=214&gp=0.jpg" alt="图片">
                    文字
                </div>

                <!--
                    4.目标元素中文本的水平对齐方式
                        - text-align
                -->
                <div style="text-align: end;">
                    测试文字
                </div>

                <!--
                    5.设置文本流入的方向，下面是可选值
                        - direction
                            - rtl
                            - ltr
                -->
                <div style="direction:rtl;">
                    测试文字
                </div>

                <!--
                    6.设置目标元素对文本内容中空白的处理方式
                        - white-space
                            - normal
                            - pre
                            - nowrap
                            - pre-wrap
                            - pre-line
                            - inherit
                -->
                <div style="white-space: inherit;">
                    测试  文字
                </div>

                <!--
                    7.目标元素中文本内容的换行方式
                        - word-break
                            - normal
                            - keep-all
                            - break-all
                -->
                <div style="word-break: break-all;">
                    abc  defghigjlmn opqrstuvwxyz
                </div>

                <!--
                    8.目标元素中文本内容的换行方式
                        - word-wrap
                            - normal
                            - break-word
                -->
                <div style="word-wrap: break-word;">
                    I am is very long text! https://github.com/tsing-document/tsing/blob/master/share/font_end/css/text.md
                </div>

            </body>
            </html>
    ```