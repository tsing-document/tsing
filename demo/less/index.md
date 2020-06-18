# 一. 初识Less
- 1.什么是 less?
    - `Less` 是 `Css` 预编译器，意思是指的是它可以扩展 `Css` 语言，添加功能。如变量，混合，函数和许多其他的技术，让你的 `Css` 更具有维护性，扩展性。

- 2.less的官网地址？
    - http://lesscss.cn/

- 3.传统写法和less的写法碰撞？
    ```html
        <div>
            <div class="container">
                <a>链接</a>
                <div class="first">
                    第一层
                    <div class="second">
                        第二层
                    </div>
                </div>
            </div>
        </div>
    ```
    - 传统写法？
        ```css
            .container {
                background-color: blue;
            }

            .container .first {
                background-color: blueviolet;
            }

            .container .first .second {
                background-color: red;
            }
        ```
    - less 写法
        ```less
            .container {
                background-color: blue;
                .first {
                    background-color: blueviolet;
                    .second {
                        background-color: yellow;
                    }
                }
            }
        ```

- 4.less的注释？
    ```less
        /***/

        //
    ```

# 二. 变量
- 1.普通的变量
    - 1.变量的定义方式？
        - @
    - 2.实例
        - less 编写
            ```less
                //编译前：
                @blue: #5B83AD;

                #header {
                    color: @blue;
                };

                //编译结果：
                #header {
                    color: #5B83AD;
                };
            ```
    - 3.由于变量只能定义一次，实际上他们就是 `常量`。

- 2.作为选择器和属性名
    - 1.变量的使用方式使用？
        - @{变量名}
    - 2.实例：
        ```less
            //编译前
            @mySelectot: width;

            .@{mySelectot} {
                @{mySelectot}: 960px;
                height: 500px;
            }；

            //编译后
            .width {
                width: 960px;
                height: 500px;
            }
        ```

- 3.作为Url
    - 1.作为url定义方式？
        - 使用时，使用 “” 将变量的指扩起来，使用时同样将变量以 @{变量名} 的方式使用
    - 2.实例：
        ```less
            //编译前
            @myUrl: "http://tsing.info/";

            body{
                background: #4cdca9 url("@{myUrl}test.png") no-repeat; 
            }

            //编译后
            body{
                background: #4cdca9 url("http://tsing.info/test.png") no-repeat; 
            }
        ```

- 4.延迟加载
    - 什么是延迟加载？
        - 变量是延迟加载的，在使用前不一定预先声明。

- 5.定义多个相同名称的变量时
    - 在定义一个变量两次时，只会使用最后定义的变量， less会从当前作用域中向上搜索，这个行为类似 css 中定义中使用使用最后定义的属性值。
    - 这个测试一下

# 三. 混合
- 1.普通混合
    - 什么是混合？
        - 混合就是一种将一系列的属性从一个规则集中引入混合到另一个规则集的方式。
    - 实例：
        ```html
            <div>
                <div class="container">
                    <h1>青衣</h1>
                    <h2>tsing</h2>
                </div>
            </div>
        ```
        ```less
            .font_h {
                background-color: turquoise;
            }

            h1 {
                color: yellow;
                .font_h;
            }

            h2 {
                color: violet;
                .font_h;
            }
        ```

- 2.不带输出的混合
    - 什么是不带输出的混合？
        - 如果你想要创建一个混合集，但是不想让他输出到你的样式中
    - 实例：
        ```html
            <div>
                <div class="container">
                    <h1>青衣</h1>
                    <h2>tsing</h2>
                </div>
            </div>
        ```
        ```less
            .font_h() {
                background-color: turquoise;
            }

            h1 {
                color: yellow;
                .font_h;
            }

            h2 {
                color: violet;
                .font_h;
            }
        ```   

- 3.带选择器的混合
    ```html
        <div>
            <div class="container">
                <button>点我</button>
            </div>
        </div>
    ```
    ```less
        .my-hover-mixin {
            &:hover {
                border: 2px solid red;
            }
        }

        button {
            .my-hover-mixin;
        }
    ```

- 4.带参数的混合
    ```html
        <div>
            <div class="container">
                <button>点我</button>
            </div>
        </div>
    ```
    ```less
        .border(@color) {
            border: 1px solid @color;
        }

        button {
            &:hover {
            .border(red)
            }
        }
    ```

- 5.带参数并且又默认值
    ```html
        <div>
            <div class="container">
                <button>点我</button>
            </div>
        </div>
    ```
    ```less
        .border(@color:red) {
            border: 1px solid @color;
        }

        button {
            &:hover {
            .border(green)
            }
        }
    ```


- 6.带多个参数的混合
    - 什么是多参数？
        > 1.一个组合可以带多个参数，参数之间可以用分号分割  
        > 2.但是推荐使用分号分割，因为逗号分割符合有两个意思，他可以解释为 `minxins` 参数分割符或者css列表分割符合
    - 定义多个具有相同名称和参数数量的混合
        - 定义多个具有相同名称和参数数量的 `minxins` 是合法的，`less` 会使用它可以应用的属性，如果使用 `minxins` 的时候只带一个参数，比如 `minxin(red)` 这个属性会导致所有的 `minxin` 都会使用强制使用这个明确的参数。

- 7.命名参数
    - 什么是命名参数？
        - 引用 `mixin` 时可以通过参数名称而不是参数的位置来为 `minxin` 提供值。
    - 实例:
        ```html
            <div>
                <div class="container">
                    <div class="name">命名参数</div>
                </div>
            </div>
        ```
        ```less
            .minxin(@color: red; @margin: 10px; @padding: 20px) {
                color: @color;
                margin: @margin;
                padding: @padding;
            }

            .name{
                .minxin
            }
        ```

- 8.@arguments变量

- 9.匹配模式

- 10.得到混合中文变量的返回值
    ```html
        <div>
            <div>
                <div class="return-value">返回值</div>
            </div>
        </div>
    ```
    ```less
        .average(@x, @y) {
            @average: ((@x + @y)/2);
        }

        .return-value {
            .average(100px, 200px);
            padding: @average;
            background: turquoise;
        }
    ```

# 四. 嵌套规则
- 1.什么是嵌套规则？
    - 嵌套规则是它模仿了 `Html` 的结构，让我们的 `css` 代码更加简介明了清晰。
- 2.实例：
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