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
                <div style="margin: 10px; background-color: yellow; border: 2px solid black;">
                    元素选择器 - 元素选择器
                </div>
            </body>
            </html>
        ```
    - 效果：  
        ![元素选择器](./images/1594374018517.jpg)
    - 属性选择器：
        - E {...}
            ```css
                <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title></title>
                    <style type="text/css">
                    </style>
                </head>
                <body>
                    <div style="margin: 10px; background-color: yellow; border: 2px solid black;">
                        属性选择器 - E {...}
                    </div>
                </body>
                </html>
            ```
        - 效果：
            <body>
                <div style="margin: 10px; background-color: yellow; border: 2px solid black;">
                    属性选择器 - E {...}
                </div>
            </body>
            </html>