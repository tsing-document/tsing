### 字体相关属性：
- 概要：
    - font
    - color
    - font-family
    - font-size
        - xx-small
        - x-small
        - small
        - medium
        - large
        - x-large
        - xx-large
        - larger
        - smaller
        - length
    - font-size-adjust
    - font-stretch
        - narrower
        - wider
    - font-style
        - normal
        - italic
        - oblique
    - font-weight
    - text-decoration
        - none
        - blink
        - underline
        - line-through
        - overline
    - font-variant
        - normal
        - small-caps
    - text-shadow
    - text-transform
        - normal
        - capitaliza
        - uppercase
        - lowercase
    - line-height
    - letter-spacing
    - word-spacing

- 语法：
    ```css
        /* 1.控制文字的颜色 */
        color

        /* 2.设置文字的字体 */
        font-family

        /* 3.设置字体的大小，下列是可选值 */
        font-size
            - xx-small
            - x-small
            - small
            - medium
            - large
            - x-large
            - xx-large
            - larger
            - smaller
            - length

        /* 4.改变文字的横向拉伸，下面是可选值 */
        font-stretch
            - narrower
            - wider

        /* 5.设置文字的风格，下面是可选值 */
        font-style
            - normal
            - italic
            - oblique

        /* 6.设置字体是否加粗 */
        font-weight

        /* 7.设置文字是否有修饰线，下面是可选值 */
        text-decoration
            - none
            - blink
            - underline
            - line-through
            - overline
        
        /* 8.设置文字的大写字母的格式，下面是可选值 */
        font-variant
            - normal
            - small-caps

        /* 9.设置文字的大小写，下面是可选值  */
        text-transform
            - normal
            - capitaliza
            - uppercase
            - lowercase
        
        /* 10.设置字体的行高 */
        line-height

        /* 11.设置字体之间的字符之间的间隔 */
        letter-spacing

        /* 12.单词之间的间隔 */
        word-spacing

        /* 13.对不同字体进行字体尺寸进行微调 */
        font-size-adjust

        /* 14.设置阴影效果 */
        text-shadow

        /* 15.符合属性，将下列的详细的属性进行组合 */
        font
    ```

- 案例：
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 字体 </title>
            <style type="text/css">
                #aa {
                    font-size: 16pt;
                    font-family: "Courier New";
                    font-size-adjust: 0.41;
                }
                
                #bb {
                    font-size: 16pt;
                    font-family: "Roman";
                    font-size-adjust: 0.66;
                }

                #cc {
                    font-size: 16pt;
                    font-family: "Impact";
                    font-size-adjust: 0.93;
                }
            </style>
        </head>
        <body>
            <!-- 1.控制文字的颜色 color -->
            <span style="color: #888888;">测试文字 color: #888888;</span><br/>
            <span style="color: red;">测试文字 color: red;</span><br/>

            <!-- 2.设置文字的字体 font-family -->
            <span style="font-family: '隶书';">测试文字 font-family: '隶书';</span><br/>

            <!-- 3.设置字体的大小 font-size -->
            <span style="font-size: 34pt;">测试文字 font-size: 34pt;</span><br/>
            <span style="font-size: xx-small;">测试文字 font-size: xx-small</span><br/>
            <span style="font-size: x-small;">测试文字 font-size: x-small;</span><br/>
            <span style="font-size: samll;">测试文字 font-size: samll</span><br/>
            <span style="font-size: medium;">测试文字 font-size: medium</span><br/>
            <span style="font-size: large">测试文字 font-size: large</span><br/>
            <span style="font-size: x-large;">测试文字 font-size: x-large;</span><br/>
            <span style="font-size: xx-large;">测试文字 font-size: xx-large</span><br/>
            <span style="font-size: larger;">测试文字 font-size: larger</span><br/>
            <span style="font-size: smaller">测试文字 font-size: smaller</span><br/>
        
            <!-- 4.改变文字的横向拉伸 font-stretch-->
            <span style="font-stretch: narrower;">测试文字 font-stretch: narrower;</span><br/>
            <span style="font-stretch: wider;">测试文字 font-stretch: narrower;</span><br/>

            <!-- 5.设置文字的风格 font-style -->
            <span style="font-style: italic;">测试文字 font-style: italic;</span><br/>

            <!-- 6.设置字体是否加粗 font-weight -->
            <span style="font-weight: bold;">测试文字 font-weight: bold;</span><br/>
            <span style="font-weight: 900;">测试文字 font-weight: 900;</span><br/>

            <!-- 7.设置文字是否有修饰线 text-decoration-->
            <span style="text-decoration: blink;">测试文字 text-decoration: blink;</span><br/>
            <span style="text-decoration: underline;">测试文字 text-decoration: underline;</span><br/>
            <span style="text-decoration: line-through;">测试文字 text-decoration: line-through;</span><br/>

            <!-- 8.设置文字的大写字母的格式 font-variant -->
            <span style="font-variant: small-caps;">测试文字 font-variant: small-caps;</span><br/>

            <!-- 9.设置文字的大小写 text-transform -->
            <span style="text-transform: uppercase;">测试文字 text-transform: uppercase;</span><br/>
            <span style="text-transform: capitalize;">测试文字 text-transform: capitalize;</span><br/>

            <!-- 10.设置字体的行高 line-hight -->
            <span style="line-height: 50pt;">测试文字 line-height: 50pt;</span><br/>

            <!-- 11.设置字体之间的字符之间的间隔 letter-spacing -->
            <span style="letter-spacing: 50pt;">测试文字 letter-spacing: 50pt;</span><br/>

            <!-- 12.单词之间的间隔 word-spacing -->
            <span style="word-spacing: 30pt;">测试文字 word-spacing: 30pt;</span><br/>

            <!-- 13.对不同字体进行字体尺寸进行微调 font-size-adjust *** 只有火狐支持-->
            <div id="aa">The Yellow River flows into the sea</div>
            <div id="bb">The Yellow River flows into the sea</div>
            <div id="cc">The Yellow River flows into the sea</div>

            <!-- 14.设置阴影效果 text-shadow -->
            <!-- 解释：
                color: 指定阴影的颜色。
                xoffset: 指定阴影在横向上的偏移。
                yoffset: 指定阴影在纵向上的偏移。
                redius:  指定阴影的模糊半径。
            -->
            <p style="text-shadow: red  5px 5px 2px;">测试文字 - text-shadow</p>
            <p style="text-shadow: 5px 5px 2px; color: blue;">测试文字 - text-shadow</p>
            <p style="text-shadow: -5px -5px 2px; color: gray;">测试文字 - text-shadow</p>
            <p style="text-shadow: -5px 5px 2px; color: yellow;">测试文字 - text-shadow </p>
            <p style="text-shadow: 5px -5px 2px; color: green;">测试文字 - text-shadow</p>
        </body>
        </html>
    ```
