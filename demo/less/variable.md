# 变量
- 概述
    - 概念：
        - 将通用的样式抽取出来。
        ```less
            //原始的 less 
            a,
            .link {
                color: #428bca;
            }
            .widget {
                color: #fff;
                background: #428bca;
            }

            //提取变量
            // 变量
            @link-color:        #428bca; // sea blue
            @link-color-hover:  darken(@link-color, 10%);

            // 用法
            a,
            .link {
                color: @link-color;
            }
            a:hover {
                color: @link-color-hover;
            }
            .widget {
                color: #fff;
                background: @link-color;
            }
        ```

- Variable Interpolation(变量插值)
    - 概念：
        - 在上面的例子主要集中于 css 规则中使用变量管理值，实际上他们还可以用在其他地方，比如选择器名称，属性名，urls以及`@import`语句中。

- Selectors(选择器)
    ```less
        // 变量
        @mySelector: banner;

        // 用法
        .@{mySelector} {
            font-weight: bold;
            line-height: 40px;
            margin: 0 auto;
        }

        //编译后
        .banner {
            font-weight: bold;
            line-height: 40px;
            margin: 0 auto;
        }
    ```
- URLs(路径)
    ```less
        //变量
        @images: "../img";

        //使用
        body {
            color: #444;
            background: url("@{images}/white-sand.png");
        }
    ```
- Import statements(导入语句)
    ```less
        // 变量
        @themes: "../../src/themes";

        // 用法
        @import "@{themes}/tidal-wave.less";
    ```
- Properties(属性)
    ```less
        //编译前
            @property: color;

            .widget {
                @{property}: #0ee;
                background-@{property}: #999;
            }
        //编译后
            .widget {
                color: #0ee;
                background-color: #999;
            }
    ```
- Variable Names(变量名)
    ```less
        //编译前
            @fnord:  "I am fnord.";
            @var:    "fnord";
            content: @@var;
        //编译后
            content: "I am fnord.";
    ```
- Lazy Loading(延迟加载)
    ```less

    ```
- default variables(默认变量)