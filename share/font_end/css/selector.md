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
    - 元素选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>元素选择器</title>
                <style type="text/css">
                </style>
            </head>
            <body>
                <div style="width: 100%;
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;">
                    元素选择器 - 元素选择器
                </div>
            </body>
            </html>
        ```
    - 属性选择器：
        - E {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                    </style>
                </head>
                <body>
                    <div style="width: 100%;
                                height: 100px;
                                background-color: yellow;
                                border: 2px solid black;">
                        属性选择器 - E {...}
                    </div>
                </body>
                </html>
            ```
        - E[attr] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        div[id] {
                            width: 100%;
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                        }
                    </style>
                </head>
                <body>
                    <div id="java">
                        属性选择器 - 指定该css样式具有的 attr 属性的 e 元素起作用。
                    </div>
                </body>
                </html>
            ```
        - E[attr=value] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        div[id=javaee] {
                            width: 100%;
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                        }
                    </style>
                </head>
                <body>
                    <div id="javaee"></div>
                </body>
                </html>
            ```
        - E[attr～=value] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        div[id~=java] {
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                            margin: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div id="java ee"></div>
                    <div id="java script"></div>
                </body>
                </html>
            ```
        - E[attr |=value ] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        /*
                            选择 lang 属性值以 “en” 开头的元素b，并设置样式。
                        */
                        div[lang |= java] {
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                            margin: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div lang="java-ee"></div>
                    <div lang="java-script"></div>
                </body>
                </html>
            ```
        - E[att^="value"] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        /*
                            设置 class 属性值以 "test" 开头的所有 div 元素的背景色。
                        */
                        div[class ^= java] {
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                            margin: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div class="java-ee"></div>
                    <div class="java-script"></div>
                </body>
                </html>
            ```
        - E[att$="value"] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        /*
                            设置 class 属性值以"java"结尾的所有div元素的背景颜色。
                        */
                        div[class $= java] {
                            height: 100px;
                            background-color: red;
                            border: 2px solid black;
                            margin: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div class="ee-java"></div>
                    <div class="script-java"></div>
                </body>
                </html>
            ```
        - E[attr*=value] {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>属性选择器</title>
                    <style type="text/css">
                        div[id*=java] {
                            height: 100px;
                            background-color: yellow;
                            border: 2px solid black;
                            margin: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div id="javaee"></div>
                    <div id="javascript"></div>
                </body>
                </html>
            ```
    - ID选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>ID选择器</title>
                <style type="text/css">
                    #se {
                        height: 100px;
                        background-color: red;
                        border: 2px solid black;
                        margin: 10px;
                    }
                </style>
            </head>
            <body>
                <div id="se"></div>
            </body>
            </html>
        ```
    - class选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>class选择器</title>
                <style type="text/css">
                    .se {
                        height: 100px;
                        background-color: green;
                        border: 2px solid black;
                        margin: 10px;
                    }
                </style>
            </head>
            <body>
                <div class="se"></div>
            </body>
            </html>
        ```
    - 包含选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>包含选择器</title>
                <style type="text/css">
                    div {
                            background-color: #dddddd;
                        }
                    div .a {
                        background-color: #888;
                    }
                </style>
            </head>
            <body>
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
            </body>
            </html>
        ```
    - 子选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>子选择器</title>
                <style type="text/css">
                    div {
                            background-color:darkslategray;
                            margin: 5px;
                        }
                    div>.a {
                        background-color: red;
                    }
                </style>
            </head>
            <body>
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
            </body>
            </html>
        ```
    - 组合选择器：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>组合选择器</title>
                <style type="text/css">
                    div, p, section {
                            background-color:darkslategray;
                            margin: 5px;
                        }
                </style>
            </head>
            <body>
                <div>
                    组合选择器 - div 元素。
                </div>
                <p>
                    组合选择器 - p 元素。
                </p>
                <section>
                    组合选择器 - section 元素。
                </section>
            </body>
            </html>
        ```
    - 兄弟选择器(css3新增)：
        ```css
            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="UTF-8">
                <meta name="viewport" content="width=device-width, initial-scale=1.0">
                <title>css3 新增兄弟选择器</title>
                <style type="text/css">
                /*
                    匹配id为android的元素后面、class属性为long的兄弟节点。
                */
                    #android ~ .long {
                            background-color:red;
                        }
                </style>
            </head>
            <body>
                <div>
                    第一行
                </div>
                <div class="long">
                    第二行
                </div>
                <div id="android">
                    第三行
                </div>
                <p class="long">
                    第三行
                </p>
                <div class="long">
                    第四行
                </div>
            </body>
            </html>
        ```

