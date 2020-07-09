# html5&css3&js讲义
## 第一章：及联样式和css选择器
- 一、css 概述以及引入：
    - 简介：
        - css 的全称是 `Casading Style Sheet`(及联样式单)，也称为层叠样式单，主要控制让页面更加漂亮。
    - 优点：
        - 表达效果丰富。
        - 文档信息检索。
        - 便于信息检索。
        - 可读性好。
    - 发展历史：
        - css 1.0：
            - 1996年12月，css1.0 作为第一个正式规范面世，其中已经加入可字体、颜色等属性。
        - css 2.0：
            - 2004年2月， css2.1 对原来的css2.0进行了一些小范围的修改，删除了一些浏览器支持不成熟的属性。css2.1可以认为是css2.0修订版。
        - css 3.0：
            - 2010年，css规范推出，这个版本的css完善了前面的css的一些不足。
    - 引入：
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

- 二、css选择器
    - [css选择器](./selector.md)
    - [伪元素选择器](./pseudo.selector.md)

## 第二章：字体和文本相关属性
    - [字体](./typeface.md)