# 第一章：及联样式和css选择器
- ### 一、css 概述：
    - 简介：
        - css 的全称是 `Casading Style Sheet`(及联样式单)，也称为层叠样式单，主要控制让页面更加漂亮。
    - 优点：
        - 表达效果丰富。
        - 文档信息检索。
        - 便于信息检索。
        - 可读性好。

- ### 二、发展历史：
    - css 1.0：
        - 1996年12月，css1.0 作为第一个正式规范面世，其中已经加入可字体、颜色等属性。
    - css 2.0：
        - 2004年2月， css2.1 对原来的css2.0进行了一些小范围的修改，删除了一些浏览器支持不成熟的属性。css2.1可以认为是css2.0修订版。
    - css 3.0：
        - 2010年，css规范推出，这个版本的css完善了前面的css的一些不足。

- ### 三、引入css：
    - 链接外部样式文件:
        ```css
            <!-- 在 header 中添加 -->
            <link type="text/css" rel="stylesheet" href="样式文件的URL"/>
        ```
    - 导入外部样式文件：
        ```css
            <style type="text/css">
                @import "outer.css";
                @import "mycss.css";
            </style>
        ```
    - 使用内部样式定义：
        ```css
            <style type="text/css">
                样式单文件定义
            </style>
        ```
    - 使用行内样式：
        ```css
            <!-- 在标签体内 -->
            style="属性名1:属性值1;属性名2:属性值2;"
        ```

- ### 四、css 选择器：
    - css `Hello world`：
        ```css
            Selector {
                属性名1: 属性值1;
                属性名2: 属性值2;
            }
        ```
    - 解释：
        - Select(选择器)：
            - 选择器决定该样式定义对那些元素起作用。
        - { 属性名1: 属性值1; 属性名2：属性值2 }(属性定义)：
            - 属性定义部分决定这些样式器怎样的作用。
    - 选择器：
        - 元素选择器：
            - 语法：
                ```css
                    E {...} /* 其中 E 代表有效的 html 元素名 */
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>元素选择器</title>
                        <style type="text/css">
                            body {
                                background-color: greenyellow;
                            }

                            div {
                                background-color: red;
                            }
                        </style>
                    </head>
                    <body>
                        <div>
                            元素选择器
                        </div>
                    </body>
                    </html>
                ```
        - 属性选择器：
            - 语法：
                ```css
                    E {...} /* 指定该 css 样式对所有的 e 元素起作用。*/
                    E[attr] /* {...}: 执行该 css 样式对所有 e 元素起作用。*/
                    E[attr=value] {...} /* 指定该 css 样式对所有包含attr属性，且attr属性为value的 e 元素起作用。*/
                    E[attr ~=value] { ... } /* 指定该css样式对所有包含 attr 属性，且attr属性的值为空格隔开的系列值，其中某个值为value的e元素起作用。*/
                    E[attr =value] { ... } /* 指定该css样式对所有包含attr属性，且attr属性的值为以连字符分隔的系列值，其中第一个值为value的tag元素起作用。*/
                    E[att^="value"] {...} /* 指定该css样式对所有包含attr属性，且attr的属性值为以value开头的字符串的e元素起作用。*/
                    E[att$="value"] {...} /* 指定该css样式对所有包含attr属性，且attr属性的值为以value结尾的字符串的e元素起作用。*/
                    E[att*="value"] {...} /* 指定该css样式对所有包含attr属性，且attr属性的值为包含value的字符串的e元素起作用。*/
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>属性选择器</title>
                        <style type="text/css">
                            div {
                                width: 330px;
                                height: 30px;
                                background-color: #eee;
                                border: 1px solid black;
                                padding: 10px;
                            }

                            /* 对有id属性起作用的选择器 */
                            div[id] {
                                background-color: #aaa;
                            }

                            /* 对有id属性值包含xx的div元素起作用 */
                            div[id*=xx] {
                                background-color: #999;
                            }

                            /* 对有id属性值以xx开头的div元素起作用 */
                            div[id^=xx] {
                                background-color: #555;
                            }

                            /* 对有id属性值等于xx的div元素起作用 */
                            div[id=xx] {
                                background-color: #111;
                            }
                        </style>
                    </head>
                    <body>
                        <div>没有任何属性的div</div>
                        <div id="a">待ID属性的div元素</div>
                        <div id="zzxx">id属性值包含xx子字符串的div</div>
                        <div id="xxyy">id属性值以xx开头div元素</div>
                        <div id="xx">id属性值为xx的div元素</div>
                    </body>
                    </html>
                ```
        - id选择器：
            - 语法：
                ```css
                    #idValue {}
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>id选择器</title>
                        <style type="text/css">
                            div {
                                width: 330px;
                                height: 30px;
                                background-color: #eee;
                                border: 1px solid black;
                                padding: 10px;
                            }

                            #xx {
                                background-color: #222;
                            }
                        </style>
                    </head>
                    <body>
                        <div>没有任何属性的div</div>
                        <div id="xx">id属性值</div>
                    </body>
                    </html>
                ```
        - class选择器：
            - 语法：
                ```css
                    [E].classValue { ... }
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>class选择器</title>
                        <style type="text/css">
                            .myclass {
                                width: 330px;
                                height: 30px;
                                background-color: #dddddd;
                            }

                            div.myclass {
                                background-color: red;
                            }
                        </style>
                    </head>
                    <body>
                        <div class="myclass">
                            class为myclass的div元素
                        </div>
                        <p class="myclass">
                            class为myclass的p元素
                        </p>
                    </body>
                    </html>
                ```
        - 包含选择器：
            - 语法：
                ```css
                    Selector1 Selector2 { ... } /* 其中 Selector1 Selector2 都是有效的选择器 */
                ```
            - html：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>包含选择器</title>
                        <style type="text/css">
                            div {
                                width: 330px;
                                height: 30px;
                                background-color: #dddddd;
                                margin: 5px;
                            }

                            div .a {
                                width: 200px;
                                height: 35px;
                                border: 2px dotted black;
                                background-color: #888;
                            }
                        </style>
                    </head>
                    <body>
                        <div>
                            没有任何属性的 div 元素
                        </div>
                        <div>
                            <section>
                                <div class="a">
                                    处于 div 之内且 class 属性为 a 的元素
                                </div>
                            </section>
                        </div>
                        <p class="a">
                            没有处于 div 之内，但 class 属性为a的元素。
                        </p>
                    </body>
                    </html>
                ```
        - 子选择器：
            - 语法：
                ```css
                    Selector1>Selector2 { ... } /* 其中 Selector1 Selector2 都是有效的选择 */
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>子选择器</title>
                        <style type="text/css">
                            div {
                                width: 330px;
                                height: 30px;
                                background-color: #dddddd;
                                margin: 5px;
                            }

                            div>.a {
                                width: 200px;
                                height: 35px;
                                border: 2px dotted black;
                                background-color: #888;
                            }
                        </style>
                    </head>
                    <body>
                        <div>
                            没有任何属性的 div 元素
                        </div>
                        <div>
                            <p class="a">
                            class属性为a且div的子节点的元素
                            </p>
                        </div>
                        <div>
                            <section>
                                <p class="a">
                                    class属性为a且处于div内部的元素
                                </p>
                            </section>
                        </div>
                    </body>
                    </html>
                ```
            - 注意：
                - 包含选择器与子选择器有点相似，他们之间存在如下的区别：
                    - 包含选择器：
                        - 只要目标选择器位于外部选择器对应的元素内部，即使是其“孙子元素也可”；
                    - 子选择器：
                        - 要求目标选择器必须作为外部选择器对应的元素直接子元素才行；
        - css3 新增的兄弟选择器
            - 语法：
                ```css
                    Selector1 ~ Selector2 { ... } /* 其中Selector1 Selector2 都是有效的选择 */
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>兄弟选择器</title>
                        <style type="text/css">
                            #android ~ .long {
                                background-color: #00ff00;
                            }

                        </style>
                    </head>
                    <body>
                        <div>
                            疯狂 java 讲义
                        </div>
                        <div class="long">
                            轻量级java ee 企业应用实战
                        </div>
                        <div id="android">
                            疯狂andriod讲义
                        </div>
                        <p class="long">
                            经典java ee企业应用实战
                        </p>
                        <div class="long">
                            疯狂 html5/ css3 / js
                        </div>
                    </body>
                    </html>

                ```
            - 注意：
                - 兄弟选择器匹配与 Selector1 对应元素后面、能匹配Selector2的兄弟节点。
        - 选择器组合：
            - 语法：
                ```css
                    Selector1,Selector2,Selector3,... {...}
                ```
            - 案例：
                ```html
                    <!DOCTYPE html>
                    <html lang="en">
                    <head>
                        <meta charset="UTF-8">
                        <meta name="viewport" content="width=device-width, initial-scale=1.0">
                        <title>选择器组合</title>
                        <style type="text/css">
                            div, .a, #abc {
                                width: 200px;
                                height: 35px;
                                border: 2px dotted black;
                                background-color: #888;
                            }

                        </style>
                    </head>
                    <body>
                        <div>
                            没有任何属性的div元素
                        </div>
                        <div class="a">
                            class属性是a的元素
                        </div>
                        <div id="abc">
                            id为abc的元素
                        </div>
                    </body>
                    </html>
                ```
        - 伪元素选择器：
            - 语法：
                ```css
                    /* 伪元素选择器如下 */
                    :first-lettle
                        - 该选择器对应的css样式对指定对象内的第一个字符起作用。
                    :first-line
                        - 该选择器对应的css样式对指定对象内的第一行起作用。
                    :before
                        - 该选择器与内容相关属性结合使用，用于在指定对象内部的前端插入内容。
                    :after
                        - 该选择器与内容相关的属性结合使用，用于在指定对象内部的后端插入内容。
                ```
            - 案例：
                - first-lettle
                    ```html
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title>:first-letter</title>
                            <style type="text/css">
                                span {
                                    display: block;
                                }
                                /*
                                    span 元素里第一个字母加粗、变红，由于 span 是行内元素，因此需要先把行内元素变成块级元素。
                                */
                                span:first-letter {
                                    color: #f00;
                                    font-size: 20pt;
                                }
                                
                                section:first-letter {
                                    color: #00f;
                                    font-size: 30pt;
                                    font-weight: bold;
                                }

                                p:first-letter {
                                    color: #00f;
                                    font-size: #00f;
                                    font-weight: bold;
                                }
                            </style>
                        </head>
                        <body>
                            <span>
                                abc
                            </span>
                            <section>
                                其实我就是一个程序员。
                            </section>
                            <p>
                                疯狂java讲义
                            </p>
                        </body>
                        </html>
                    ```
                - :first-line
                    ```html
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title>:first-line</title>
                            <style type="text/css">
                                span {
                                    display: block;
                                }
                                /*
                                    span 元素里第一个字母加粗、变红，由于 span 是行内元素，因此需要先把行内元素变成块级元素。
                                */
                                span:first-line {
                                    color: #f00;
                                    font-size: 20pt;
                                }
                                
                                section:first-line {
                                    color: #00f;
                                    font-size: 30pt;
                                    font-weight: bold;
                                }

                                p:first-line {
                                    color: #00f;
                                    font-size: #00f;
                                }
                            </style>
                        </head>
                        <body>
                            <span>
                                abc
                                <br/>
                                xyz
                            </span>
                            <section>
                                白日衣衫尽，
                                <br/>
                                黄河入海流。
                            </section>
                            <p style="width: 160px;">
                                疯狂 java 讲义
                            </p>
                        </body>
                        </html>
                    ```
        - 内容相关的属性：
            - 语法：
                ```css
                    /* css 支持的内容相关的属性 */
                    include-source:
                        - 该属性的值应为 url，插入绝对或者相对路径，目前还没有浏览器支持该属性。
                    content:
                        - 该属性的值可以是字符串、url、attr(alt)、counter(name)、counter(name,list-style-type)、open-quote、close-quote等格式。该属性用于指定元素之前或之后插入指定内容。
                    qiotes:
                        - 该属性用于content属性定义open-quote和close-quote，该属性的值可以是两个以空格分隔字符串，其中前面的字符串是 open-quote,后面的字符串是close-quote。
                    counter-increment:
                        - 该属性用于定义一个计数器。该属性的值就是所定义的计数器的名称。
                    - counter-reset:
                        - 该属性用于对指定的计数值复位。
                ```
            - 案例：
                - 插入内容：
                    ```html
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title> content </title>
                            <style type="text/css">
                                span {
                                    display: block;
                                }
                                /*
                                    指定向 div 元素内部的前端插入 content 属性对应的内容
                                */
                                div>div:before {
                                    content: '插入的内容';
                                    color: #f00;
                                    font-size: 20pt;
                                    font-weight: bold;
                                }

                            </style>
                        </head>
                        <body>
                            <div>
                                <div>白日依山进，</div>
                                <div>黄河入海流。</div>
                                <div>欲穷千里目，</div>
                                <div>更上一层楼。</div>
                            </div>
                        </body>
                        </html>
                    ```
                - 插入图像：
                    ```html
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title> 插入图像 </title>
                            <style type="text/css">
                                /*
                                    指定向 div 元素内部的后端插入 content 属性对应的内容
                                */
                                div>div:after {
                                    content: url('wc.gif');
                                }

                            </style>
                        </head>
                        <body>
                            <div>
                                <div>白日依山进，</div>
                                <div>黄河入海流。</div>
                                <div>欲穷千里目，</div>
                                <div>更上一层楼。</div>
                            </div>
                        </body>
                        </html>
                    ```
                - 只插入部分元素：
                    ```html
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title> 部分插入图片 </title>
                            <style type="text/css">
                                /*
                                    指定向 div 元素内部的后端插入 content 属性对应的内容
                                */
                                div>div.no:after {
                                    content: url('wc.gif');
                                }

                            </style>
                        </head>
                        <body>
                            <div>
                                <div class="no">白日依山进，</div>
                                <div class="no">黄河入海流。</div>
                                <div>欲穷千里目，</div>
                                <div>更上一层楼。</div>
                            </div>
                        </body>
                        </html>
                    ```
                - 配合 quotes 属性执行插入：
                    ```css
                        <!DOCTYPE html>
                        <html lang="en">
                        <head>
                            <meta charset="UTF-8">
                            <meta name="viewport" content="width=device-width, initial-scale=1.0">
                            <title> 配合quotes属性执行插入 - 添加符合</title>
                            <style type="text/css">
                                /*
                                    定义 open-quote 为 <<， close为 >> 
                                */
                                div>div {
                                    quotes: "<<" ">>";
                                }

                                div>div:before {
                                    content: open-quote;
                                }

                                div>div:after {
                                    content: close-quote;
                                }

                            </style>
                        </head>
                        <body>
                            <div>
                                <div>白日依山进，</div>
                                <div>黄河入海流。</div>
                                <div>欲穷千里目，</div>
                                <div>更上一层楼。</div>
                            </div>
                        </body>
                        </html>
                    ```
        - 配合 counter-increment 属性添加编号：
            ```html
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title> 配合counter-increment属性添加编号</title>
                    <style type="text/css">
                
                        div>div {
                            counter-increment: myconter;
                        }

                        div>div:before {
                            content: counter(myconter) '.';
                        }


                    </style>
                </head>
                <body>
                    <div>
                        <div>白日依山进，</div>
                        <div>黄河入海流。</div>
                        <div>欲穷千里目，</div>
                        <div>更上一层楼。</div>
                    </div>
                </body>
                </html>
            ```
        - 使用自定义编号：
            ```css
                /* 通过 counter(name, list-style-type) 来实现自定义编号*/
                decimal:
                    - 阿拉伯数字，默认值
                disc:
                    - 实心圆
                circle:
                    - 空心圆
                square:
                    - 方块
                lower-roman:
                    - 小写罗马数字
                upper-roman:
                    - 大写罗马数字
                lower-alpha:
                    - 小写英文字母
                upper-alpha:
                    - 大写英文字母
                none:
                    - 不使用项目符合
                cjk-ideographic:
                    - 浅白色的表的数字
                georgian:
                    - 传统的乔治数字
                lower-greek:
                    - 基本的希腊小写字母
                hebrew:
                    - 传统的希伯莱数字
                hiragana:
                    - 日本平假名字符
                hiragana-iroha:
                    - 日本平假名序号
                katakana:
                    - 日本片假名字符
                katakana-iroha:
                    - 日本片假名序号
                lower-latin:
                    - 小写拉丁字母
                upper-latin:
                    - 大写拉丁字母
            ```
            ```html
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title> 自定义编号 </title>
                    <style type="text/css">
                
                        div>div {
                            counter-increment: myconter;
                        }

                        div>div:before {
                            content: '第' counter(myconter, lower-greek) '行.';
                        }

                    </style>
                </head>
                <body>
                    <div>
                        <div>白日依山进，</div>
                        <div>黄河入海流。</div>
                        <div>欲穷千里目，</div>
                        <div>更上一层楼。</div>
                    </div>
                </body>
                </html>
            ```

