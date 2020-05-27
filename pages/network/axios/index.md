# Axios

## 简介:
- 概念:
    - axios 是一个基于 `Promise`, 用于浏览器和 `nodejs` 的 `HTTP` 客户端
- 使用方式:
    - 从浏览器中创建 XMLHttpRequest
    - 从 node.js 发出 http 请求
    - 支持 Promise API
    - 拦截请求和响应
    - 转换请求和响应数据
    - 取消请求
    - 自动转换JSON数据
    - 客户端支持防止 CSRF/XSRF

## 引入方式:
- npm:
    ```bash
        $ npm install axios
    ```

- bower:
    ```bash
        $ bower install axios
    ```

- cdn:
    ```bash
        <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    ```

## 示例:
- Get:
    ```bash
        ## 入门
        const axios = require('axios');

        const openApi = 'https://api.storeapi.net/api/67/176?format=json&sign=6fd73a7bca096bb135aaf36c9c79dd11&appid=2233';

        axios.get(openApi).then(function (response) {
            // handle success
            console.log(response);
        })
        .catch(function (error) {
            // handle error
            console.log(error);
        })
        .then(function () {
            // always executed
        });
    ```

    ```bash
        ## 也可以用下面实现
        axios.get('https://api.storeapi.net/api/67/176', {
                params: {
                    format: 'json',
                    sign: '6fd73a7bca096bb135aaf36c9c79dd11',
                    appid:2233
                }
        }).then(function (response) {
                console.log(response);
        }).catch(function (error) {
                console.log(error);
        }).then(function () {
                // always executed
        }); 
    ```

    ```bash
        ## 使用 await / async 请求
        const axios = require('axios');

        const openApi = 'https://api.storeapi.net/api/67/176?format=json&sign=6fd73a7bca096bb135aaf36c9c79dd11&appid=2233';

        async function getUser() {
            try {
                const response = await axios.get(openApi);
                console.log(response);
            } catch (error) {
                console.error(error);
            }
        }
        getUser();
    ```

- Post:
    ```bash
        const axios = require('axios');

        const openApi = 'https://tying.info/menus';

        axios.post(openApi, {
            name: 'cesjo',
            sequence: 10
        })
        .then(function (response) {
            console.log(response);
        })
        .catch(function (error) {
            console.log(error);
        });
    ```

- 合并请求:
    ```bash
        const axios = require('axios');

        function getMenus() {
            return axios.get('https://tying.info/menus?current=1&size=10');
        }

        function getMenu3() {
            return axios.get('https://tying.info/menus?current=1&size=10');
        }

        axios.all([getMenus(),getMenu3()]).then(axios.spread(function (userResp,reposResp) {

            // 上面两个请求都完成后，才执行这个回调方法
            console.log('User', userResp.data);
            console.log('Repositories', reposResp.data);
        }));
    ```

## Axios Api:
- Get:
    ```bash
        const axios = require('axios');
        const openApi = 'https://tying.info/menus?current=1&size=10';

        axios({ method: 'get', url: openApi}).then(
            function (response) {
                console.log(response);
            }
        );

    ```

- Post:
    ```bash
        const axios = require('axios');

        axios({
        method: 'post',
        url: 'https://tying.info/menus',
        data: {
            name: 'cesjo',
            sequence: 10
        }
        });
    ```

- 请求方法别名:
    - 注意:
        - 当使用别名方法时, `url`, `method`, `data` 等配置不需要配置
    - axios.request(config)
    - axios.get(url[, config])
    - axios.delete(url[, config])
    - axios.head(url[, config])
    - axios.options(url[, config])
    - axios.post(url[, data[, config]])
    - axios.put(url[, data[, config]])
    - axios.patch(url[, data[, config]])

- 并发:
    - 处理并发的请求
        - axios.all(合并请求)
        - axios.spread（回调）

- 创建实例:
    ```bash
        const instance = axios.create({
            baseURL: 'https://some-domain.com/api/',
            timeout: 1000,
            headers: {'X-Custom-Header': 'foobar'}
        });

        ## 通过 axios.create 调用接口

        const axios = require('axios');

        const instance = axios.create({
            baseURL: 'https://tying.info/',
            timeout: 1000
        });

        async function getMenus () {
        const res = await instance.get('/menus?current=1&size=10');
        console.log(res);
        }

        getMenus();
    ```

- 实例方法:
    - axios#request(config)
    - axios#get(url[, config])
    - axios#delete(url[, config])
    - axios#head(url[, config])
    - axios#options(url[, config])
    - axios#post(url[, data[, config]])
    - axios#put(url[, data[, config]])
    - axios#patch(url[, data[, config]])
    - axios#getUri([config])

- 请求配置:
    ```bash
        {
            ## `url` 是用于请求的服务器的  `url`
            url: '/user',

            ## `method` 是发出请求是要使用的请求方法
            method: 'get', // default

            // `baseURL` will be prepended to `url` unless `url` is absolute.
            // It can be convenient to set `baseURL` for an instance of axios to pass relative URLs
            // to methods of that instance.
            baseURL: 'https://some-domain.com/api/',

            ## `transformRequest` 允许在将请求数据发送到服务器之前将其进行更改,但是这仅适用于方法 `put`, `post`, 'patch' 数组中的最后一个函数必须返回一个字符串或者缓冲区的 array buffer,或者数据流,你可以修改 headers 对象
            transformRequest: [function (data, headers) {
                // Do whatever you want to transform the data

                return data;
            }],

            // `transformResponse` allows changes to the response data to be made before
            // it is passed to then/catch
            transformResponse: [function (data) {
                // Do whatever you want to transform the data

                return data;
            }],

            ## `headers` 是客户端发送的
            headers: {'X-Requested-With': 'XMLHttpRequest'},

            ## `params` 是路径上的参数
            params: {
                ID: 12345
            },

            // `paramsSerializer` is an optional function in charge of serializing `params`
            // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
            paramsSerializer: function (params) {
                return Qs.stringify(params, {arrayFormat: 'brackets'})
            },

            // `data` is the data to be sent as the request body
            // Only applicable for request methods 'PUT', 'POST', and 'PATCH'
            // When no `transformRequest` is set, must be of one of the following types:
            // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
            // - Browser only: FormData, File, Blob
            // - Node only: Stream, Buffer
            data: {
                firstName: 'Fred'
            },

            // `timeout` specifies the number of milliseconds before the request times out.
            // If the request takes longer than `timeout`, the request will be aborted.
            timeout: 1000, // default is `0` (no timeout)

            // `withCredentials` indicates whether or not cross-site Access-Control requests
            // should be made using credentials
            withCredentials: false, // default

            // `adapter` allows custom handling of requests which makes testing easier.
            // Return a promise and supply a valid response (see lib/adapters/README.md).
            adapter: function (config) {
                /* ... */
            },

            // `auth` indicates that HTTP Basic auth should be used, and supplies credentials.
            // This will set an `Authorization` header, overwriting any existing
            // `Authorization` custom headers you have set using `headers`.
            auth: {
                username: 'janedoe',
                password: 's00pers3cret'
            },

            // `responseType` indicates the type of data that the server will respond with
            // options are 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
            responseType: 'json', // default

            // `responseEncoding` indicates encoding to use for decoding responses
            // Note: Ignored for `responseType` of 'stream' or client-side requests
            responseEncoding: 'utf8', // default

            // `xsrfCookieName` is the name of the cookie to use as a value for xsrf token
            xsrfCookieName: 'XSRF-TOKEN', // default

            // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
            xsrfHeaderName: 'X-XSRF-TOKEN', // default

            // `onUploadProgress` allows handling of progress events for uploads
            onUploadProgress: function (progressEvent) {
                // Do whatever you want with the native progress event
            },

            // `onDownloadProgress` allows handling of progress events for downloads
            onDownloadProgress: function (progressEvent) {
                // Do whatever you want with the native progress event
            },

            // `maxContentLength` defines the max size of the http response content in bytes allowed
            maxContentLength: 2000,

            // `validateStatus` defines whether to resolve or reject the promise for a given
            // HTTP response status code. If `validateStatus` returns `true` (or is set to `null`
            // or `undefined`), the promise will be resolved; otherwise, the promise will be
            // rejected.
            validateStatus: function (status) {
                return status >= 200 && status < 300; // default
            },

            // `maxRedirects` defines the maximum number of redirects to follow in node.js.
            // If set to 0, no redirects will be followed.
            maxRedirects: 5, // default

            // `socketPath` defines a UNIX Socket to be used in node.js.
            // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
            // Only either `socketPath` or `proxy` can be specified.
            // If both are specified, `socketPath` is used.
            socketPath: null, // default

            // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
            // and https requests, respectively, in node.js. This allows options to be added like
            // `keepAlive` that are not enabled by default.
            httpAgent: new http.Agent({ keepAlive: true }),
            httpsAgent: new https.Agent({ keepAlive: true }),

            // 'proxy' defines the hostname and port of the proxy server.
            // You can also define your proxy using the conventional `http_proxy` and
            // `https_proxy` environment variables. If you are using environment variables
            // for your proxy configuration, you can also define a `no_proxy` environment
            // variable as a comma-separated list of domains that should not be proxied.
            // Use `false` to disable proxies, ignoring environment variables.
            // `auth` indicates that HTTP Basic auth should be used to connect to the proxy, and
            // supplies credentials.
            // This will set an `Proxy-Authorization` header, overwriting any existing
            // `Proxy-Authorization` custom headers you have set using `headers`.
            proxy: {
                host: '127.0.0.1',
                port: 9000,
                auth: {
                username: 'mikeymike',
                password: 'rapunz3l'
                }
            },

            // `cancelToken` specifies a cancel token that can be used to cancel the request
            // (see Cancellation section below for details)
            cancelToken: new CancelToken(function (cancel) {
            })
            }
    ```

- 响应配置:
    ```bash
        {
            // `data` is the response that was provided by the server
            data: {},

            // `status` is the HTTP status code from the server response
            status: 200,

            // `statusText` is the HTTP status message from the server response
            statusText: 'OK',

            // `headers` the headers that the server responded with
            // All header names are lower cased
            headers: {},

            // `config` is the config that was provided to `axios` for the request
            config: {},

            // `request` is the request that generated this response
            // It is the last ClientRequest instance in node.js (in redirects)
            // and an XMLHttpRequest instance the browser
            request: {}
        }
    ```
    - 当用 `then` 时候, 你能获取相应数据:
    ```bash
        const axios = require('axios');

        const instance = axios.create({
        baseURL: 'https://tying.info/',
        timeout: 1000
        });

        async function getMenus () {
        instance.get('/menus?current=1&size=10').then(function (response) {
            console.log(response.data);
            console.log(response.status);
            console.log(response.statusText);
            console.log(response.headers);
            console.log(response.config);
        });
        }

        getMenus();
    ```

- 默认配置:
    - 全局配置:
        ```bash
            axios.defaults.baseURL = 'https://api.example.com';
            axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
            axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
        ```

    - 自定义示例配置:
        ```bash
            ## Set config defaults when creating the instance
            const instance = axios.create({
                baseURL: 'https://api.example.com'
            });

            ## Alter defaults after instance has been created
            instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;

        ```

    - 拦截器:
        ```bash
            ## 添加请求的拦截器
            axios.interceptors.request.use(function (config) {
                ## Do something before request is sent
                return config;
            }, function (error) {
                ## Do something with request error
                return Promise.reject(error);
            });

            ## 添加响应的拦截器
            axios.interceptors.response.use(function (response) {
                ## Do something with response data
                return response;
            }, function (error) {
                ## Do something with response error
                return Promise.reject(error);
            });

            ## 删除拦截器
            const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
            axios.interceptors.request.eject(myInterceptor);

            ## 将拦截器添加到实例中
            const instance = axios.create();
            instance.interceptors.request.use(function () {/*...*/});
        ```

- 处理错误:
    ```bash
        axios.get('/user/12345').catch(function (error) {
                if (error.response) {
                // The request was made and the server responded with a status code
                // that falls out of the range of 2xx
                console.log(error.response.data);
                console.log(error.response.status);
                console.log(error.response.headers);
                } else if (error.request) {
                // The request was made but no response was received
                // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
                // http.ClientRequest in node.js
                console.log(error.request);
                } else {
                // Something happened in setting up the request that triggered an Error
                console.log('Error', error.message);
                }
                console.log(error.config);
        });

        ## 校验错误状态
        axios.get('/user/12345', {
            validateStatus: function (status) {
                return status < 500; // Reject only if the status code is greater than or equal to 500
            }
        })
    ```

## 框架整合 - vue-axios
- 安装:
    - npm install --save axios vue-axios

- 添加你的文件:
    ```bash
        import Vue from 'vue'
        import axios from 'axios'
        import VueAxios from 'vue-axios'

        Vue.use(VueAxios, axios)
    ```

- 用法: 
    ```bash
        Vue.axios.get(api).then((response) => {
            console.log(response.data)
        })

        this.axios.get(api).then((response) => {
            console.log(response.data)
        })

        this.$http.get(api).then((response) => {
            console.log(response.data)
        })
    ```

## 框架整合
- TODO: