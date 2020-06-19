# Yarn包管理工具
- 快速入门
    - 简介：
        - Yarn 对你的代码来说就是一个包管理器。它可以让你使用并分享全世界的代码。Yarn 能够快速、安全、 并可靠地完成这些工作，所以你不用有任何担心。代码通过 包（package） (或者称为 模块（module）) 的方式来共享。 一个包里包含所有需要共享的代码，以及描述包信息的文件，称为 package.json 。

    - 安装：
        - Homebrew
            ```bash
                brew install yarn
            ```
        - MacPorts
            ```bash
                sudo port install yarn
            ```

    - 升级：
        ```bash
            brew upgrade yarn
        ```

    - 检测：
        ```bash
            yarn --version
        ```

    - 使用：
        - 创建新的项目：
            ```bash
                yarn init

                question name (yarn-project): demo-yarn
                question version (1.0.0):
                question description: demo
                question entry point (index.js):
                question repository url:
                question author: tsing
                question license (MIT):
                question private:

                //package.json
                {
                    "name": "demo-yarn",
                    "version": "1.0.0",
                    "description": "demo",
                    "main": "index.js",
                    "author": "tsing",
                    "license": "MIT"
                }
            ```

        - 添加依赖包
            ```bash
                yarn add [package]
                yarn add [package]@[version]
                yarn add [package]@[tag]
            ```
        
        - 将依赖添加到不同的类别中
            ```bash
                //分别添加到 devDependencies、peerDependencies 和 optionalDependencies 类别中：

                yarn add [package] --dev
                yarn add [package] --peer
                yarn add [package] --optional
            ```

        - 升级安装包
            ```bash
                yarn upgrade [package]
                yarn upgrade [package]@[version]
                yarn upgrade [package]@[tag]
            ```
        
        - 移除依赖包
            ```bash
                yarn remove [package]
            ```

        - 安装项目的全部依赖
            ```bash
                yarn || yarn install
            ```

- Yarn 工作流
    - 创建新项目
        - 创建
            ```bash
                yarn init
            ```
        - 打开一个交互的表单，用于创建一个新的项目，并且填写相关的问题
            ```bash
                name (your-project):
                version (1.0.0):
                description:
                entry point (index.js):
                git repository:
                author:
                license (MIT):
            ```
        - 生成的 `package.json`
            ```json
                {
                    "name": "my-new-project",
                    "version": "1.0.0",
                    "description": "My New Project description.",
                    "main": "index.js",
                    "repository": {
                        "url": "https://example.com/your-username/my-new-project",
                        "type": "git"
                    },
                    "author": "Your Name <you@example.com>",
                    "license": "MIT"
                }
            ```
    - 管理依赖
        - 添加依赖项
            ```bash
                //如果要使用其他软件包，则首先需要将其添加为依赖项。为此，您应该运行：
                    yarn add [package]

                //这将自动将添加[package]到您的依赖中 package.json。它还会更新您的内容yarn.lock以反映更改。

                //package.json
                {
                    "name": "demo-yarn",
                    "version": "1.0.0",
                    "description": "demo",
                    "main": "index.js",
                    "author": "tsing",
                    "license": "MIT",
                    "dependencies": {
                        "lodash": "^4.17.15"
                    }
                }

                //您还可以使用标志添加其他 类型的依赖项：
                yarn add --dev 添加到 devDependencies
                yarn add --peer 添加到 peerDependencies
                yarn add --optional 添加到 optionalDependencies

                //您可以通过指定依赖项版本或 标记来指定要安装的软件包版本。
                yarn add [package]@[version]
                yarn add [package]@[tag]
            ```

        - 升级依赖
            ```bash
                yarn upgrade [package]
                yarn upgrade [package]@[version]
                yarn upgrade [package]@[tag]

                //这将升级您package.json和您的yarn.lock文件。
                    {
                        "name": "my-package",
                        "dependencies": {
                        -    "package-1": "^1.0.0"
                        +    "package-1": "^2.0.0"
                        }
                    }
            ```
        
        - 删除依赖
            ```bash
                yarn remove [package]
            ```

    - 安装依赖
        - `yarn install` 用于安装项目的所有的依赖，从项目 `package.json` 文件中检索依赖关系，并将其存储在 `yarn.lock` 文件中。
        - 安装依赖的场景：
            - 将项目刚刚从仓库中检索出来之后
            - 其他同事添加了相关的依赖
        - 安装选件
            - 有许多安装依赖的选项：
                - 1.安装所有依赖项：yarn或yarn install
                - 2.安装软件包的一个版本和唯一一个版本： yarn install --flat
                - 3.强制重新下载所有软件包： yarn install --force
                - 4.仅安装生产依赖项： yarn install --production
    
    - 和版本管理工具协同工作
        - 基础 
            - 为了使人们成功开发或使用您的软件包，您需要确保将所有必需的文件都签入源代码控制系统。
        - 所需文件
            - package.json：这具有您软件包的所有当前依赖关系。
            - yarn.lock：这将为您的软件包存储每个依赖项的确切版本。
            - 提供软件包功能的实际源代码。
    
    - 持久集成整合：
        - ？

- 从npm迁移到yarn
    - 简介：
        - 如果想要从 `npm` 转换成 `yarn`，可以先将 `node_modules` 删除，然后再执行 `yarn`。

    - npm 和 yarn 的 cli 对比
        |  npm   | yarn  |
        |  ----  | ----  |
        | npm install | yarn add |
        | (N/A) | yarn add --flat |
        | (N/A) | yarn add --har  |
        | npm install --no-package-lock | yarn add --no-lockfile |
        | (N/A) | yarn add --pure-lockfile |
        | npm install [package] --save | yarn add [package] |
        | npm install [package] --save-dev | yarn add [package] --dev |
        | (N/A) | yarn add [package] --peer |
        | npm install [package] --save-optional | yarn add [package] --optional |
        | npm install [package] --save-exact | yarn add [package] --exact |
        | (N/A) | yarn add [package] --tilde |
        | npm install [package] --global | yarn global add [package] |
        | npm update --global | yarn global upgrade |
        | npm rebuild | yarn add --force |
        | npm uninstall [package] | yarn remove [package] |
        | npm cache clean | yarn cache clean [package] |
        | rm -rf node_modules && npm install | yarn upgrade |
        | npm version major | yarn version --major |
        | npm version minor | yarn version --minor |
        | npm version patch | yarn version --patch |

- 配置

- 离线镜像

- 工作区

- plug`n`play

- cli 命令

- 依赖 & 版本

- 创建一个包
    - todo: 这个后面发布自己的工具包整理