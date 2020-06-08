# 安装及应用
- ## 安装:
    - `Taro` 项目是基于 `node`, 确保 `node` 环境 (>=8.0.0), 可以推荐用 `nvm` 来管理 `node` 不同版本 。

- ## CLI工具安装
    - 首先, 使用 `npm` 或者 `yarn` 全局安装 `@tarojs/cli`, 或者直接使用 `npx`:
        ```bash
            # 使用 npm 安装 CLI
            $ npm install -g @tarojs/cli
            # OR 使用 yarn 安装 CLI
            $ yarn global add @tarojs/cli
            # OR 安装了 cnpm，使用 cnpm 安装 CLI
            $ cnpm install -g @tarojs/cli
        ```

- ## 注意事项
    - 如果安装的过程中出现 `sass` 相关的安装错误， 请先安装 `mirror-config-china` 后重试。
        ```bash
            $ npm install -g mirror-config-china
        ```

- ## 项目初始化
    - 使用命令创建模板项目
        ```bash
            $ taro init myApp
        ```
    
    - npm 5.2+ 也可以在不全局安装的情况下使用 `npx` 创建模板项目
        ```bash
            npx @tarojs/cli init myApp
        ```

- ## 启动项目
    - 微信小程序
        ```bash
            # yarn
            $ yarn dev:weapp
            $ yarn build:weapp
            # npm script
            $ npm run dev:weapp
            $ npm run build:weapp
            # 仅限全局安装
            $ taro build --type weapp --watch
            $ taro build --type weapp
            # npx 用户也可以使用
            $ npx taro build --type weapp --watch
            $ npx taro build --type weapp
        ```

- ## 快速创建新页面
    - Taro create --name [页面名称]