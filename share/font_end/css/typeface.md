### 字体相关属性：
- 语法：
    - font：
        - 这是一个复合属性，其属性的值形如 `font-style`、`font-variant`、`font-weight`、`font-size`、`line-height`、`font-family` 的复合属性值。使用 `font` 属性可以同时控制文字的样式、字体粗体、字体大小、字体等属性，为了更具体的进行控制，通常不建议使用该属性。
    - color：
        - 该属性用于控制文字颜色，该属性的值可以是任何有效的颜色值，包含字符串类型的颜色名、十六进制的颜色值，或使用 `reb()` 函数设置 RGB 值等，甚至包含 css3.0 提供的 hsl 颜色值等。
    - font-family：
        - 设置文字的字体，因为字体需要浏览器内嵌字体的支持，该属性可以设置多个显示字体，浏览器按该属性指定的多个字体一次搜索，以优先找到的字体来显示文字。多个属性值之间用（，）隔开。
    - font-size：
        - 该属性用于设置文字的字体大小，此处的字体大小既可以是相对的字体大小，也可以是绝对的字体大小。该属性支持如下的属性值。
            - xx-small：
                - 绝对字体尺寸。最小字体。
            - x-small：
                - 绝对字体尺寸。较小字体。
            - samll：
                - 绝对字体尺寸。小字体。
            - medium：
                - 绝对字体尺寸。正常大小的字体。这是默认值。
            - large：
                - 绝对字体尺寸。大字体。
            - x-large：
                - 绝对字体尺寸。较大字体。
            - xx-large：
                - 绝对字体尺寸。最大字体。
            - larger：
                - 相对字体尺寸。相对于父元素的字体进行相对增大。
            - smaller：
                -  相对字体尺寸。相对于父元素中的字体进行相对减少。
            - length：
                - 直接设置字体大小。该值既可以设置为一个百分比值，意味着该字体大小是父元素中字体大小的百分比值：也可设置为一个数值 + 长度单位。
    - font-size-adjust：
        - 该属性用于控制对不同字体尺寸进行微调。该属性可以指定为 none(不进行任何调整)或用一个数值代表调整比例。
    - font-stretch：
        - 该属性用于改变文字横向的拉伸，该属性的默认值为normal，既不拉伸。还有两个属性值，是 narrower 和 wider，前者是横向压缩，后者是横向拉伸。
    - font-style：
        - 该属性用于设置文字风格，是否采用斜体等。该属性的常用属性有normal、italic、oblique,这些属性值依次表示设置文字正常、斜体、倾斜字体。
    - font-weight：
        - 该属性用于设置字体是否加粗。该属性的值表示加粗的程度用 lighter、norrmal、bold、bolder 等属性值表示。
    - text-decoration：
        - 该属性用于控制文字是否有修饰线，如下滑线等。该属性的值有 none（无修饰）、blink（闪烁）、underline（下画线）、line-through（中画线）和overline（上画线）。
    - font-variant：
        - 该属性用于设置文字的写字母的格式。
    - text-shadow：
        - 设置文字的阴影效果。
    - text-transform：
        - 设置文字的大小。
    - line-hight：
        - 设置字体的行高。
    - letter-spacing：
        - 设置字符之间的间隔。
    - word-spacing：
        - 设置单词之间的间隔。

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
            <!-- 字体颜色 color -->
            <span style="color: #888888;">测试文字 color: #888888;</span><br/>
            <span style="color: red;">测试文字 color: red;</span><br/>

            <!-- 文字字体 font-family -->
            <span style="font-family: '隶书';">测试文字 font-family: '隶书';</span><br/>

            <!-- 文字大小 font-size -->
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
        
            <!-- 文字横向拉伸 font-stretch-->
            <span style="font-stretch: narrower;">测试文字 font-stretch: narrower;</span><br/>
            <span style="font-stretch: wider;">测试文字 font-stretch: narrower;</span><br/>

            <!-- 设置文字风格 font-style -->
            <span style="font-style: italic;">测试文字 font-style: italic;</span><br/>

            <!-- 设置字体是否加粗 font-weight -->
            <span style="font-weight: bold;">测试文字 font-weight: bold;</span><br/>
            <span style="font-weight: 900;">测试文字 font-weight: 900;</span><br/>

            <!-- 设置字体是否有修饰线 text-decoration-->
            <span style="text-decoration: blink;">测试文字 text-decoration: blink;</span><br/>
            <span style="text-decoration: underline;">测试文字 text-decoration: underline;</span><br/>
            <span style="text-decoration: line-through;">测试文字 text-decoration: line-through;</span><br/>

            <!-- 设置文字大写字母格式 font-variant -->
            <span style="font-variant: small-caps;">测试文字 font-variant: small-caps;</span><br/>

            <!-- 设置文字的大小写 text-transform -->
            <span style="text-transform: uppercase;">测试文字 text-transform: uppercase;</span><br/>
            <span style="text-transform: capitalize;">测试文字 text-transform: capitalize;</span><br/>

            <!-- 设置文字的行高 line-hight -->
            <span style="line-height: 50pt;">测试文字 line-height: 50pt;</span><br/>

            <!-- 设置字符之间的间隔 letter-spacing -->
            <span style="letter-spacing: 50pt;">测试文字 letter-spacing: 50pt;</span><br/>

            <!-- 设置单词之间的间隔 word-spacing -->
            <span style="word-spacing: 30pt;">测试文字 word-spacing: 30pt;</span><br/>

            <!-- 设置阴影 text-shadow -->
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

            <!-- 微调字体 font-size-adjust *** 只有火狐支持-->
            <div id="aa">The Yellow River flows into the sea</div>
            <div id="bb">The Yellow River flows into the sea</div>
            <div id="cc">The Yellow River flows into the sea</div>
        </body>
        </html>

    ```
