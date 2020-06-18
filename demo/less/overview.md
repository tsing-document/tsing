# Less 概览

## 语言特性
- ### Variables(变量)
    - 概念
        - 变量只能定义一次，实际上他们就是 `常量`。

    ```html
        <div class='variables'>变量</div>
    ```

    ```less
        //less
        @nice-blue: #5B83AD;
        @light-blue: @nice-blue + #290;

        .variables {
            color: @light-blue;
        }

        //out
        .variables {
            color: #6c94be;
        }
    ```

- ### Mixins(混合)
    - 概念：
        - 混合就是一种将一系列属性从一个规则集引入(`混合`)到另一个规则集中的方式。

    ```html
        <div>
            <div class='first'>
                <a>
                    第一个
                </a>
            </div>
            <div class='second'>
                <a>
                    第二个
                </a>
            </div>
        </div>
    ```

    ```less
        .bordered {
            border-top: dotted 2px blue;
            border-bottom: solid 2px blue;
        }

        .first {
            padding-bottom: 100px ;
            a {
                color: red;
                .bordered;
            }
        }

        .second a {
            color: red;
            .bordered;
        }
    ```

- ### Nested rules(嵌套规则)
    - 概念：
        - Less 为我们提供了嵌套的能力，而不是合并在样式表中。
    ```html
        <div>
            <div class='first-floor'>
                <div class='desc'>
                    嵌套规则
                </div>
            </div>
        </div>
    ```
    ```less
        .first-floor {
            width: 100px;
            height: 100px;
            background-color: chartreuse;
            .desc {
                background-color: chocolate;
                width: 50px;
                height: 50px;
            }
        }
    ```

- ### Operations(运算)
    - 概念：
        - 任何数值，颜色和变量都可以进行运算。
    ```html
        <div>
            <div class='operations'>
                运算
            </div>
        </div>
    ```
    ```less
        @base: 50px;
        @filler: @base * 2;
        @other: @base + @filler;

        .operations {
            width: 100px;
            height: @other;
            background-color: aqua;
        }
    ```

- ### Function(函数)
    - 概念：
        - Less 提供了许多用于转换颜色，处理字符串和进行算术运算的函数。

    ```html
        <div>
            <div class='functions'>
                函数
            </div>
        </div>
    ```
    ```less
        @base: #f04615;
        @width: 0.5;

        .functions {
            width: percentage(@width); // returns `50%`
            color: saturate(@base, 5%);
            background-color: spin(lighten(@base, 25%), 8);
        }
    ```

- ### Namespaces and Accessors(命名空间和访问器)
    - 概念：
        - 不要将它与 css `@namespace` 或 `namespace` 选择器混为一谈。
    ```less
        #bundle {
            .button {
                display: block;
                border: 1px solid black;
                background-color: grey;
                &:hover {
                background-color: white
                }
            }
            .tab { ... }
            .citation { ... }
        }

        // 如果想在 `header a` 中混合 `.button` 类，这样可以这样做
        #header a {
            color: orange;
            #bundle > .button;
        }
    ```

- ### Scope(作用域)
    - 概述：
        - Less 中作用域和编程语言中的作用域概念非常相似。首先会在局部查找变量和混合，如果没找到，编译器就会在父作用域中查找，以此类推。
    ```less
        @var: red;
        #page {
            @var: white;
            #header {
                color: @var; // white
            }
        }

        //等同

        @var: red;
        #page {
            #header {
                color: @var; // white
            }
            @var: white;
        }
    ```

- ### Comments(注释)
    - 概述：
        - 可以使用块注释和行注释。
    ```less
        /*
         * 块注释
         *
        /
        //行注释
    ```

- ### 伪类
- ### 媒体查询
