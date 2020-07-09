# css 选择器：
- 概要：
    - 元素选择器
    - 属性选择器：
        - E {...} 
        - E[attr] {...}
        - E[attr=value] {...}
        - E[attr ~=value] {...}
        - E[attr =value] { ... } 
        - E[att^="value"] {...}
        - E[att$="value"] {...}
        - E[att*="value"] {...} 
    - ID选择器
    - class选择器
    - 包含选择器
    - 子选择器
    - 组合选择器
    - 伪元素选择器 //这个另外文章讲解
    - 伪类选择器(css3.0新增) //这个另外文章讲解
    - 兄弟选择器(css3.0新增)

- 基本使用：
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

- 语法：
    ```css
        /* 1.元素选择器 */
        E {...}

        /* 2.属性选择器 */
        E {...} /* 指定该 css 样式对所有的 e 元素起作用。*/
        E[attr] /* {...}: 执行该 css 样式对所有 e 元素起作用。*/
        E[attr=value] {...} /* 指定该 css 样式对所有包含attr属性，且attr属性为value的 e 元素起作用。*/
        E[attr ~=value] { ... } /* 指定该css样式对所有包含 attr 属性，且attr属性的值为空格隔开的系列值，其中某个值为value的e元素起作用。*/
        E[attr =value] { ... } /* 指定该css样式对所有包含attr属性，且attr属性的值为以连字符分隔的系列值，其中第一个值为value的tag元素起作用。*/
        E[att^="value"] {...} /* 指定该css样式对所有包含attr属性，且attr的属性值为以value开头的字符串的e元素起作用。*/
        E[att$="value"] {...} /* 指定该css样式对所有包含attr属性，且attr属性的值为以value结尾的字符串的e元素起作用。*/
        E[att*="value"] {...} /* 指定该css样式对所有包含attr属性，且attr属性的值为包含value的字符串的e元素起作用。*/

        /* 3.ID选择器 */
        #idValue {}

        /* 4.class选择器 */
        [E].classValue { ... }

        /* 5.包含选择器 */
        Selector1 Selector2 { ... } /* 其中 Selector1 Selector2 都是有效的选择器 */

        /* 6.子选择器 */
        Selector1>Selector2 { ... } /* 其中 Selector1 Selector2 都是有效的选择 */
        - 注意：
            - 包含选择器与子选择器有点相似，他们之间存在如下的区别：
                - 包含选择器：
                    - 只要目标选择器位于外部选择器对应的元素内部，即使是其“孙子元素也可”；
                - 子选择器：
                    - 要求目标选择器必须作为外部选择器对应的元素直接子元素才行；
        
        /* 7.组合选择器 */
        Selector1,Selector2,Selector3,... {...}
    ```
- 案例：
    ```html
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title> 选择器 </title>
            <style type="text/css">
                /* 1.元素选择器 */
                div {
                    margin: 10px;
                    background-color: yellow;
                    border: 2px solid black;
                }

                /* 2.属性选择器 */
                    /* E {...} */
                    div {
                        margin: 10px;
                        background-color: yellow;
                        border: 2px solid black;
                    }

                    /* E[attr] {...} */
                    div[id] {
                        background-color: brown;
                    }

                    /* E[attr=value] {...} */
                    div[id*=xxx] {
                        background-color: chartreuse;
                    }

                    /* E[attr ~=value] {...} */
                    div[title="title"] {
                        background-color: blue;
                    }

                    /* E[attr ｜=value] { ... } */
                    div[lang|=en] {
                        background-color:green;
                    }

                    /* E[att^="value"] {...} */
                    div[id^=yy] {
                        background-color: hotpink;
                    }

                    /* E[att$="value"] {...} */
                    div[id$=zz] {
                        background-color: khaki;
                    }

                    /* E[att*="value"] {...} */
                    div[id*=uu] {
                        background-color: lightgreen;
                    }

                /* 3.ID选择器 */
                    #aa {
                        background-color: mediumblue;
                        border: 1px solid black;
                    }
                
                /* 4.class选择器 */
                    .classSelector {
                        background: cadetblue;
                    }
                
                /* 5.包含选择器 */
                    div {
                        background-color: #dddddd;
                    }

                    div .a {
                        background-color: #888;
                    }

                /* 6.子选择器 */
                    div {
                        background-color:darkslategray;
                        margin: 5px;
                    }

                    div>.a {
                        background-color: darkslategray;
                    }

                /* 7.组合选择器 */
                    section, h1, p {
                        background-color: plum;
                    }
                
                /* 8.兄弟选择器(css3.0新增) */
                    #android ~ .long {
                        background-color: #00ff00;
                    }
                    
            </style>
        </head>
        <body>
            <!-- 1.元素选择器 -->
                <div>元素选择器 - 元素选择器</div>

            <!-- 2.属性选择器 -->
                <!-- E {...} -->
                <div>
                    属性选择器 - 指定该css样式对所有的 e 元素起作用。
                </div>

                <!-- E[attr] {...} -->
                <div id="java">
                    属性选择器 - 指定该css样式具有的 attr 属性的 e 元素起作用。
                </div>
                <div id="javaee">
                    属性选择器 - 指定该css样式具有的 attr 属性的 e 元素起作用。
                </div>

                <!-- E[attr=value] {...} -->
                <div id="xxx">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性为value的e元素起作用。
                </div>

                <!-- E[attr ~=value] {...} -->
                <div title="title">
                    属性选择器 - 指定该 css 样式对所有包含 attr 属性，且 attr 属性的值以空格隔开的系列值，其中某个值为 value 的 e 元素起作用。
                </div>

                <!-- E[attr ｜=value] { ... } --> 
                <div lang="en">
                    属性选择器 - 指定该css样式对所有包含attr属性，且attr属性的值为以连字符分隔的系列值，其中第一个值为 value 的 tag 元素起作用。
                </div>
                <div lang="en-us">
                    属性选择器 - Hi!
                    指定该css样式对所有包含attr属性，且attr属性的值为以连字符分隔的系列值，其中第一个值为 value 的 tag 元素起作用。
                </div>

                <!-- E[att^="value"] {...} -->
                <div id="yy">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为以value开头的字符串的 e元素起作用。
                </div>
                <div id="yy-xx">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为以value开头的字符串的 e元素起作用。
                </div>

                <!-- E[att$="value"] {...} -->
                <div id="zz">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为以value结尾的字符串的 e 元素起作用。
                </div>
                <div id="xx-zz">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为以value结尾的字符串的 e 元素起作用。
                </div>

                <!-- E[att*="value"] {...} -->
                <div id="uu">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为包含value的字符串的e元素起作用。
                </div>
                <div id="uu-zz">
                    属性选择器 - 指定该css样式对所有包含 attr 属性，且attr属性的值为包含value的字符串的e元素起作用。
                </div>
            
            <!-- 3.ID选择器 -->
                <div id="aa">
                    ID选择器 - ID选择器
                </div>

            <!-- 4.class选择器 -->
                <div class="classSelector">
                    class 选择器 - class 选择器
                </div>

            <!-- 5.包含选择器 -->
                <div>
                    包含选择器 - 没有任何属性的 div 元素
                </div>
                <div>
                    <section>
                        <div class="a">
                            包含选择器 - 处于 div 之内且 class 属性为 a 的元素
                        </div>
                    </section>
                </div>
                <p class="a">
                    包含选择器 - 没有处于 div 之内，但 class 属性为a的元素。
                </p>

            <!-- 6.子选择器 -->
                <div>
                    子选择器 - 没有任何属性的 div 元素
                </div>
                <div>
                    <p class="a">
                        子选择器 - class属性为a且div的子节点的元素
                    </p>
                </div>
                <div>
                    <section>
                        <p class="a">
                        子选择器 - class属性为a且处于div内部的元素
                        </p>
                    </section>
                </div>
            
            <!-- 7.组合选择器 -->
                <h1>
                    组合选择器 - h1标签
                </h1>
                <section>
                    组合选择器 - section
                </section>
                <p>
                    组合选择器 - p标签
                </p>

            <!-- 8.兄弟选择器(css3.0新增) -->
                <div>
                    兄弟选择器(css3.0新增) - 疯狂 java 讲义
                </div>
                <div class="long">
                    兄弟选择器(css3.0新增) - 轻量级java ee 企业应用实战
                </div>
                <div id="android">
                    兄弟选择器(css3.0新增) - 疯狂andriod讲义
                </div>
                <p class="long">
                    兄弟选择器(css3.0新增) - 经典java ee企业应用实战
                </p>
                <div class="long">
                    兄弟选择器(css3.0新增) - 疯狂 html5/ css3 / js
                </div>
        </body>
        </html>
    ```
