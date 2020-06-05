https://www.jianshu.com/p/68e849768d8e
## React 入门指南
- 知识点
    ```bash
        1. 创建项目并访问项目
        2. 整合 ts
        3. 将 function 方式修改成 class 形式
        4. 在 class 中使用嵌套表达式
        5. 在 class 中使用任何有效的 javaScript 表达式
        6. `Jsx` 也是一个表达式
        7. React元素是不可变对象, 一旦诶创建, 就无法更改他的子元素或者属性
        8. 组件 & props
        9. state和生命周期
        10. 事件处理
        11. 条件渲染

    ```

- 1.创建项目并访问项目
```bash
    # 创建项目
    npx create-react-app <project name>
    # 切换目录
    cd <project name>
    # 启动项目
    yarn start
    # 访问项目
    http://127.0.0.1:3000
```

- 2.整合ts
```bash
    # 创建新的项目使用 ts
        $ npx create-react-app <project name> --typescript
        $ # 或者
        $ yarn create react-app <project name> --typescript
    # 将 ts 添加到通过 create-react-app 创建的项目中
        $ npm install --save typescript @types/node @types/react @types/react-dom @types/jest
        $ # 或者
        $ yarn add typescript @types/node @types/react @types/react-dom @types/jest 
    # 直接将 `src` 下的 .js 文件修改成 .tsx
    # 重新启动服务
```

- 3.将 `function` 方式修改成 `class` 形式
```html
    import React from 'react';

    export default class App extends React.Component {
        render() {
            return (
                <div>
                    Hello World!
                </div>
            )
        }
    }

```

- 4.在 `class` 中使用嵌套表达式
```html
import React from "react";

export default class App extends React.Component {
    render() {
        const name = "刘语";
        return (
            <div>
                I Love You { name }!
            </div>
        )
    }
}

```

- 5.在 `class` 中使用任何有效的 `javaScript` 表达式
```html
import React from "react";

interface User {
    name: string,
    age: number,
}

export default class App extends React.Component {

    private formatUserInfo ( user: User ) {
        return `姓名:${user.name} 年龄:${user.age}`
    };

    render() {
        const user = {
            name: "刘语",
            age: 27,
        };

        return (
            <div>
                I Love You { this.formatUserInfo(user) }!
            </div>
        )
    }
}

```

- 6.`Jsx` 也是一个表达式
```html
import React from "react";

interface User {
    name: string,
    age: number,
}

export default class App extends React.Component {

    private formatUserInfo ( user: User ) {
        return `姓名:${user.name} 年龄:${user.age}`
    };

    private desc() {
        return <div>当你走进我生命的那一刻我就爱上了你!</div>
    }

    render() {
        const user = {
            name: "刘语",
            age: 27,
        };

        return (
            <div>
                I Love You { this.formatUserInfo(user) }!
                { this.desc() }
            </div>
        )
    }
}
```

- 7.React元素是不可变对象, 一旦诶创建, 就无法更改他的子元素或者属性。
    - 注意: 实际上只更新了改变的地方, 其他地方没有更新
```html
import React from "react";

interface User {
    name: string,
    age: number,
}

export default class App extends React.Component {

    componentWillMount () {
        setInterval(this.time, 1000);
    }

    readonly state = {
        time: '',
    };

    private formatUserInfo ( user: User ) {
        return `姓名:${user.name} 年龄:${user.age}`
    };

    private desc(time: string) {
        return <div>当你走进我生命的那一刻我就爱上了你! 爱上你的时间:{time}</div>
    };

    private time = () =>{
        this.setState({
            time: new Date().toLocaleTimeString()
        });
    }

    render() {
        const user = {
            name: "刘语",
            age: 27,
        };

        return (
            <div>
                I Love You { this.formatUserInfo(user) }!
                { this.desc(this.state.time) }
            </div>
        )
    }
}
```

- 8.组件 & props
```html
<!-- app.tsx -->
import React from "react";
import ImageComponent from './image.component';

export default class App extends React.Component {

    render() {
        return (
            <div>
                <ImageComponent  imageUrl={'https://s3-cn-north-1.qiniucs.com/tsing-dotbar/car.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=uRkcNoj0lCMtohr087LXm8CKB0tQPW8epyBFozCh%2F20200605%2Fcn-north-1%2Fs3%2Faws4_request&X-Amz-Date=20200605T020450Z&X-Amz-Expires=600&X-Amz-Signature=2aa93d6a817c1688dafbcd7a68e59c3097a8abbdcf9d5527610b5ac869d04407&X-Amz-SignedHeaders=host'}/>
            </div>
        )
    }
}

<!-- 组件和向组件中传值 ImageComponent.tsx -->
import React from 'react';

interface IProps {
    imageUrl: string,
}
export default class ImageComponent extends React.Component<IProps> {
    render() {

        const { imageUrl } = this.props;

        return (
            <div>
               <img src={ imageUrl } alt="图片"/>
            </div>
        )
    }
}


```

- 9.state和生命周期
    - state
        ```html
            import React from "react";

            export default class App extends React.Component {

                readonly state = {
                    name: '我爱的人是:刘语',
                };

                private handlerClick = () => {
                    this.setState({
                        name: '爱我的人是: 刘语'
                    })
                };

                render() {
                    return (
                        <div>
                            { this.state.name }
                            <button onClick={this.handlerClick}>切换喜欢的人</button>
                        </div>
                    )
                }
            }

        ```
    - 生命周期
        - 引用文章:
            - https://www.jianshu.com/p/b331d0e4b398
            - 1.挂载卸载过程  
                - 1.1 constructor()
                - 1.2 componentWillMount()
                - 1.3 componentDidMount()
                - 1.4 componentWillUnmount ()
            - 2.更新过程
                - 2.1.componentWillReceiveProps (nextProps)
                - 2.2.shouldComponentUpdate(nextProps,nextState)
                - 2.3.componentWillUpdate (nextProps,nextState)
                - 2.4.componentDidUpdate(prevProps,prevState)
                - 2.5.render()
            - 3.React新增的生命周期
                - 3.1. getDerivedStateFromProps(nextProps, prevState)
                - 3.2. getSnapshotBeforeUpdate(prevProps, prevState)


- 10.事件处理
    - 概念:
        - react 事件的命名采用小驼峰式, 而不是纯小写。
        - 使用 `JSX` 语法时需要传入一个函数作为事件处理函数, 而不是一个字符串。
    - 展示效果:
        - 在第九个案例中有demo

- 11.条件渲染
    - 