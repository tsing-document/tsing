# PM2

## 快速开始
- 1.概念：
    - `PM2` 是守护进程管理器，他将帮助你管理和保持应用程序在线。

- 2.安装：
    - 可以通过 `npm` 或者 `yarn` 安装最新的 `PM2` 版本：
        ```bash
            $ npm install pm2@latest -g
            # or
            $ yarn global add pm2
        ```

- 3.启动一个应用：
    - 先创建一个简单的`http`请求。
        ```js
            const http=require('http');

            http.createServer(function(requset,response){
                    console.log('request come',requset.url)
                    response.end('123')
            }).listen(7777)

            console.log('服务启动了~');
        ```
    - 启动服务:
        ```bash
            node 文件名.js
        ```
    - 在浏览器上访问链接 `http://ip:7777`
    - 用 `pm2` 方式启动：
        ```bash
            pm2 start http.js
        ```
    - 传递参数：
        - 指定服务的名称：
            ```bash
                pm2 start http.js --name demo-http
            ```
        - 监听应用目录的变化，一旦发生变化，自动重启。如果要精确监听、不见听的目录，最好通过配置文件:
            ```bash
                pm2 start http.js --watch
            ```
        - 如果想要应用程序达到一定内存的上限，自动重启：
            ```bash
                pm2 start http.js --max-memory-restart 20M
            ```
        - 指定日志输出的地址：
            ```bash
                pm2 start http.js --log /root/doc_test/test.log
            ```
        - 通过脚本传递额外的参数：
            ```bash
                -- arg1 arg2 arg3   //?
            ```
        - 自动重新启动之间的延迟：
            ```bash
                --restart-delay <delay in ms> //?
            ```
        - 日志的输出内容中添加上时间：
            ```bash
                pm2 start http.js --log /root/doc_test/test.log --time
            ```
        - 不要自动启动应用程序
            ```bash
                --no-autorestart
            ```
        - Specify cron for forced restart
            ```bash
                cron <cron_pattern>
            ```
        - Attach to application log
            ```bash
                --no-daemon
            ```

- 4.管理状态：
    - 管理应用程序的状态：
        ```bash
            $ pm2 restart app_name
            $ pm2 reload app_name
            $ pm2 stop app_name
            $ pm2 delete app_name

            // 也可以使用下面的方式代替 app_name
            all 所有的应用程序
            id 根据特定的进程id
        ```

- 5.列出托管的应用程序：
    ```bash
        $ pm2 [list|ls|status]
    ```

- 6.显示日志
    ```bash
        $ pm2 logs
    ```

- 7.显示终端的仪表盘
    ```bash
        $ pm2 monit
    ```

- 8.监视和诊断 web 页面
    ```bash
        $ pm2 plus
    ```

- 9.集群模式

- 10.脚本方式启动

- 11.更新 PM2:
    ```bash
        npm install pm2@lastest -g
        //更新内存中的pm2
        pm2 update
    ```
