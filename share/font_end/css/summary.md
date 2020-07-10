# css 入门普及
- css 概述以及引入：
    - 简介：
        - css 的全称是`Casading Style Sheet`(及联样式单)，也称为层叠样式单，主要控制让页面更加漂亮。
    - 优点：
        - 表达效果丰富。
        - 文档信息检索。
        - 便于信息检索。
        - 可读性好。
    - 发展历史：
        - css 1.0：
            - 1996年12月，css1.0 作为第一个正式规范面世，其中已经加入可字体、颜色等属性。
        - css 2.0：
            - 2004年2月，css2.1 对原来的 css2.0 进行了一些小范围的修改，删除了一些浏览器支持不成熟的属性。css2.0 可以认为是 css2.0 修订版。
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