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
        - class选择器：
            - 格式:
                ```css
                    /* 普通 class 选择器 */
                    .myClass {
                        属性名: 属性值;
                    }

                    /* 对 class 为 myclass 的 div 元素都起作用的 css 样式 */
                    div.myClass {
                        属性名: 属性值;
                    }
                ```
                ```html
                    <p class="myClass"></p>
                    <div class="myClass"></div>
                ```
        - 包含选择器:
            - 格式:
                ```css
                    /* 对所有的 div 元素起作用的 css 的样式 */
                    div {
                         属性名: 属性值;
                    }

                    /* 对处于 div 之内且 class 属性为 a 的元素起作用的 css 样式 */
                    div .a {
                        属性名: 属性值;
                    }
                ```
                ```html
                    <div>没有任何属性的 div 元素</div>
                    <div>
                        <section>
                            <div class="a">
                                处于 div 之内且 class 属性为 a 的元素。
                            </div>
                        </section>
                    </div>
                    <p class="a">
                        没有处于 div 之内，但 class 属性为 a 的元素。
                    </p>
                ```
        - 子选择器:
            - 格式:
                ```css
                    /* 对所有的 div 元素起作用的 css 样式 */
                    div {
                        属性名: 属性值;
                    }

                    /* 对处于 div 之内 class 属性为 a 的元素起作用的 css 样式 */
                    div>.a {
                        属性名: 属性值;
                    }
                ```
                ```html
                    <div>没有任何属性的div元素</div>
                    <div>
                        <p class="a">
                            class 属性为 a 且是 div 的子节点的元素。
                        </p>
                    </div>
                    <div>
                        <section>
                            <p class="a">
                                class 属性为 a 且处于 div 内部的元素。
                            </p>
                        </section>
                    </div>
                ```
            - 注意:
                - 包含选择器与子选择器有点类似，他们之间存在如下区别: 对于包含选择器，只要目标选择器位于外部选择器对应的元素内部，即使是其“孙子元素”也可；对于子选择器，要求目标选择器必须作为外部选择器对应的元素的直接子元素才行。
        - css3新增的兄弟选择器:
            - 格式:
                ```css
                    /* 匹配 id 为 android 的元素后面、class 属性为 long 的兄弟节点 */
                    #android ~ .long {
                        属性名: 属性值;
                    }
                ```
                ```html
                    <div>
                        疯狂 java 讲义
                    </div>
                    <div class="long">
                        轻量级java ee 企业应用实战
                    </div>
                    <div id="android">
                        疯狂 android 讲义
                    </div>
                    <p class="long">
                        经典 java ee 企业应用实战
                    </p>
                    <div id="long">
                        疯狂 html 5/ css3 / javasrcipt讲义
                    </div>
                ```
            - 解释:
                - 上面的例子中id为android的元素是“疯狂 android 讲义”，虽然该元素前面的“轻量级java ee 企业应用实战” 的 class 属性为 long, 但是它位于 “疯狂 android 讲义” 的前面，因为浏览器不会为它添加北京颜色。浏览器只为于 “疯狂 android 讲义” 的后面、class 属性为 long 的两个元素添加背景颜色。
        - 选择器组合:
            - 格式:
                ```css
                    /* 使一组样式作用于多个属性选择器上 */
                    div, .a, #abc {
                        属性名: 属性值;
                    }

                    <div>没有任何属性的 div 元素</div>
                    <p class="a">class 属性为 a 的元素</p>
                    <section id="abc">id为abc的元素</section>
                ```
            - 解释:
                - 上面所有的都会作用上。
        - 伪元素选择器:
            - 伪元素:
                ```css
                    > :first-letter:  该选择器对应的 css 样式对指定对象内的第一个字符起作用。
                    > :first-line: 该选择器对应css样式对指定对象内的第一行内容起作用。
                    > :before: 该选择器和内容相关的属性结合使用，用于在指定对象内容的前端添加内容。
                    > :after: 该选择器和内容相关的书香结合使用，用于在指定对象内部的尾端添加内容。
                ```
            - 格式:
                ```css
                    span {
                        display: block;
                    }

                    /* span 元素里的第一个字母加粗，变红。由于span是一个行内元素，需要将行内元素变成块级元素 */
                    span:first-letter {
                        color: #f00;
                        font-size: 20pt;
                    }

                    /* section 元素里的第一个字母加粗，变蓝 */
                    section:first-letter {
                        color: #00f;
                        font-size: 30pt;
                        font-weight: bold;
                    }

                    p:first-line {
                        color: #00f;
                        font-size: 40pt;
                        font-weight: bold;
                    }

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
                        font-size: 40pt;
                        font-weight: bold;
                    }
                ```
                ```html
                    <span>
                        abc<br/>
                        def
                    </span>
                    <section>
                        其实我是一个程序员<br/>
                        还是一个渣男
                    </section>
                    <p>
                        疯狂java讲义<br/>
                        这本书还没看完
                    </p>
                ```
        - 内容相关属性:
            - 格式:
                ```css
                    /* 指定向 div 元素内部的前端输入 content 属性对应的内容 */
                    div>div:before {
                        content: "插入内容";
                        color: blue;
                        font-weight: bold;
                        background-color: gray;
                    }

                    /* 指定向 div 元素内部的后端输入 content 属性对应的内容 */
                    div>div:after {
                        content: "插入内容";
                        color: blue;
                        font-weight: bold;
                        background-color: gray;
                    }

                    /* 插入图片 */
                    .pic::after {
                        content: url(https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1593680378249&di=db96d61e0a61f0fb86fdd0492c3e39c9&imgtype=0&src=http%3A%2F%2Fa2.att.hudong.com%2F36%2F48%2F19300001357258133412489354717.jpg);
                    }

                    /* 配合 quotes 属性执行插入 */
                    div>div {
                        quotes: "<<" ">>";
                    }
                    /* 指定向 div 元素内部的前端输入 content 属性对应的内容 */
                    div>div:before {
                        content: open-quote;
                        color: blue;
                        font-weight: bold;
                        background-color: gray;
                    }

                    /* 指定向 div 元素内部的前端输入 content 属性对应的内容 */
                    div>div:after {
                        content: close-quote;
                        color: blue;
                        font-weight: bold;
                        background-color: gray;
                    }
                   /* 添加编号 */
                    div>div {
                        counter-increment: mycontent;
                    }

                    div>div::before {
                        content: counter(mycontent, lower-greek);
                        font-size: 20pt;
                        column-width: bold;
                    }
                ```
                ```html
                    <div>
                        <div>
                            疯狂 java 讲义
                        </div>
                        <div>
                            疯狂 android 讲义
                        </div>
                        <div>
                            轻量级 java ee 企业应用实战
                        </div>
                        <div class="pic">
                            插入图片
                        </div>
                    </div>
                ```
        - css3新增的伪类选择器:
            - 结构性伪类选择器:
                - Selector:root:
                    - 匹配文档的根元素，在 html 文档中，根元素永远是<html.../>元素。
                - Selector:last-child:
                    - 匹配符合 Selector 选择器，而且必须是其父元素的最后一个子节点的元素。
                - Selector:first-child:
                    - 匹配符合 Selector 选择器，而且必须是其父元素的第一个子元素。
                - Selector:nth-child(n):
                    - 匹配符合 Selector 选择器，而且必须是其父元素的第 n 个子节点的元素。
                - Selector:nth-last-child(n):
                    - 匹配符合 Selector 选择器，而且必须是其父元素的倒数第 n 个子元素。
                - Selector:only-child:
                    - 匹配符合 Selector 选择器，而且必须是其父元素的唯一子节点的元素。
                - Selector:first-of-type: 
                    - 匹配符合 Selector 选择器，而且是和它同类型、同级的兄弟的元素的第一个元素。
                - Selector:last-of-type:
                    - 匹配符合 Selector 选择器，而且是和它同类型，同级的兄弟元素中的最后一个。
                - Selector:nth-of-type(n):
                    - 匹配符合 Selector 选择器，而且是和它同类型，同级的兄弟元素的第 n 个元素。 
                - Selector:nth-last-of-type(n):
                    - 匹配符合 Selector 选择器，而且是和它同类型，同级的兄弟元素的倒数第 n 个元素。
                - Selector:only-of-type:
                    - 匹配符合 Selector 选择器，而且是和它同类型，同级的兄弟元素的唯一一个元素。
                - Selector:empty:
                    - 匹配符合 Selector 选择器，而且其内部没有任何子元素的元素。
                - Selector:lang(lang):
                    - 匹配符合 Selector 选择器，而且内容是特定语言的元素。
