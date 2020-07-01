## 第一章：及联样式和css选择器
- ### 一、css 概述：
    - css 的全称是 `Casading Style Sheet`(及联样式单)，也称为层叠样式单，主要控制让页面更加漂亮。
    - 优点：
        - 表达效果丰富。
        - 文档信息检索。
        - 便于信息检索。
        - 可读性好。

- ### 二、发展历史：
    - css 1.0：
        - 1996年12月，css1.0 作为第一个正式规范面世，其中已经加入可字体、颜色等属性。
    - css 2.0:
        - 2004年2月， css2.1 对原来的css2.0进行了一些小范围的修改，删除了一些浏览器支持不成熟的属性。css2.1可以认为是css2.0修订版。
    - css 3.0:
        - 2010年，css规范推出，这个版本的css完善了前面的css的一些不足。

- ### 三、基本使用：
    - 链接外部样式文件：
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
    - 简单的 css:
        ```css
            Select {
                属性名1: 属性值1;
                属性名2: 属性值2;
            }
        ```
    - 分析:
        - Select(选择器):
            - 选择器决定该样式定义对那些元素起作用。
        - { 属性名1: 属性值1; 属性名2：属性值2 }(属性定义): 属性定义部分决定这些样式器怎样的作用。
    - 选择器:
        - 元素选择器:
            - 格式:
                ```css
                    E {...} /* 其中 E 代表有效的 html 元素名 */
                ```
        - 属性选择器:
            - 格式:
                ```css
                    > E {...}: 指定该 css 样式对所有的 e 元素起作用。
                    > E[attr] {...}: 执行该 css 样式对所有 e 元素起作用。
                    > E[attr=value] {...}: 指定该 css 样式对所有包含attr属性，且attr属性为value的 e 元素起作用。
                    > E[attr ~=value] { ... }: 指定该css样式对所有包含 attr 属性，且attr属性的值为空格隔开的系列值，其中某个值为value的e元素起作用。
                    > E[attr =value] { ... }: 指定该css样式对所有包含attr属性，且attr属性的值为以连字符分隔的系列值，其中第一个值为value的tag元素起作用。
                    > E[att^="value"] {...}: 指定该css样式对所有包含attr属性，且attr的属性值为以value开头的字符串的e元素起作用。
                    > E[att$="value"] {...}: 指定该css样式对所有包含attr属性，且attr属性的值为以value结尾的字符串的e元素起作用。
                    > E[att*="value"] {...}: 指定该css样式对所有包含attr属性，且attr属性的值为包含value的字符串的e元素起作用。
                ```
        - ID选择器:
            - 格式:
                ```css
                    /* 普通 id 选择器 */
                    #idValue { ... }

                    /* 对ID为xx的p元素起作用的css样式 */
                    p#xx {
                        border: 2px dotted black;
                        background-color: #888;
                    }
                ```