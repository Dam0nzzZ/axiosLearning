#Axios
一个基于 promise （AJAX）的网络请求库，可以用于浏览器和 node.js
————————————————
###Json server

- Get a full fake REST API with zero coding in less than 30 seconds
- 学习 axois 时可当作目标服务器进行请求操作

1. 安装 json server

```cmd
>> npm install -g json-server
```

2. 创建`db.json`虚拟服务器

```json
{
  "posts": [{ "id": 1, "title": "json-server", "author": "typicode" }],
  "comments": [{ "id": 1, "body": "some comment", "postId": 1 }],
  "profile": { "name": "typicode" }
}
```

3.启动 Json server

```cmd
>> json-server --watch db.json
```

其他操作详见https://github.com/typicode/json-server

###安装 axios

- 可使用包管理工具如`npm`,`bower`等
- 或使用 CDN`<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>`
- 详见https://axios.nodejs.cn/docs/intro

###axios 方法/属性

- `axios(config)`

  - `config`：请求配置如 url、method、data 等

  ```js
  // Send a POST request
  axios({
    method: "post",
    url: "/user/12345",
    data: {
      firstName: "Fred",
      lastName: "Flintstone",
    },
  });
  ```

- 其他
  ```js
  axios.request(config)
  axios.get(url[, config])
  axios.delete(url[, config])
  axios.head(url[, config])
  axios.options(url[, config])
  axios.post(url[, data[, config]])
  axios.put(url[, data[, config]])
  axios.patch(url[, data[, config]])
  axios.postForm(url[, data[, config]])
  axios.putForm(url[, data[, config]])
  axios.patchForm(url[, data[, config]])
  ```

###axios 响应

- 响应结构
  - `config`:发送配置对象
  - `data`:响应体对象，axios 已自动将 json 解析
  - `headers`:响应头信息
  - `request`:XMLHttpRequest 原生 AJAX 请求对象
  - `status`:响应状态码
  - `statusText`:响应状态字符串

###axios 请求配置
这些是用于发出请求的可用配置选项。 只有 url 是必需的。 如果未指定 method，请求将默认为 GET。
https://axios.nodejs.cn/docs/req_config

```js
baseURL: url结构,自动与url结合,如https://xxx/,与url:post/1，发送时将二者自动结合
transformRequest/transformResponse:对发送/响应信息进行处理
header:请求头信息配置
```

###axios 配置默认值

- 全局 axios 默认值
  ```js
  axios.defaults.baseURL = "https://api.example.com";
  axios.defaults.headers.common["Authorization"] = AUTH_TOKEN;
  axios.defaults.headers.post["Content-Type"] =
    "application/x-www-form-urlencoded";
  ```
- 自定义实例

  ```js
  // Set config defaults when creating the instance
  const instance = axios.create({
    baseURL: "https://api.example.com",
  });

  // Alter defaults after instance has been created
  instance.defaults.headers.common["Authorization"] = AUTH_TOKEN;
  ```

###拦截器

- 你可以在请求或响应被 then 或 catch 处理之前拦截它们

```js
// Add a request interceptor
//config:配置对象
//可在拦截器中修改请求对象中的信息
axios.interceptors.request.use(
  function (config) {
    // Do something before request is sent
    return config;
  },
  function (error) {
    // Do something with request error
    return Promise.reject(error);
  }
);

// Add a response interceptor
//response:axios默认回复对象
axios.interceptors.response.use(
  function (response) {
    // Any status code that lie within the range of 2xx cause this function to trigger
    // Do something with response data
    return response;
  },
  function (error) {
    // Any status codes that falls outside the range of 2xx cause this function to trigger
    // Do something with response error
    return Promise.reject(error);
  }
);
```

- 注意有多个请求/响应拦截器时，请求拦截器以堆栈形式存储（后进先出），响应拦截器以队列形式（先进先出）存储
