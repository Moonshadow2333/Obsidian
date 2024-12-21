## 前置条件

- 已安装 nodejs
- 已安装 [Laragon - portable, isolated, fast & powerful universal development environment for PHP, Node.js, Python, Java, Go, Ruby.](https://laragon.org/download/)
- 已安装 [Composer](https://getcomposer.org/download/)

## 安装

```
git clone https://github.com/kaluuma-muhammad/vue3-pinia-and-laravel-9-blog-app.git
```

## 启动项目

### 启动前端

安装依赖

```
d:
cd D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\frontend
npm install
npm run dev
```

### 启动后端

```
d:
D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend
composer update
php artisan migrate  
php artisan passport:install
php artisan serve
```

php artisan  passport:install

```
D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend>php artisan passport:install
Encryption keys generated successfully.
Personal access client created successfully.
Client ID: 1
Client secret: yr1jYd9cf7JWwftaJma4RjNOrWq2sdrOS0n3WBtr
Password grant client created successfully.
Client ID: 2
Client secret: nlrZ6YO7g0kTCHIs3VpojzsAPjHwe7ZN3Wnw58AR
```

## 问题

###  SSL certificate problem

```
Failed to download doctrine/inflector from dist: curl error 60 while downloading https://api.github.com/repos/doctrine/inflector/zipball/5817d0659c5b50c9b950feb9af7b9668e2c436bc: SSL certificate problem: unable to get local issuer certificate
```


[解决PHP cURL错误代码60：SSL证书验证失败及最佳实践指南 - 云原生实践](https://www.oryoy.com/news/jie-jue-php-curl-cuo-wu-dai-ma-60-ssl-zheng-shu-yan-zheng-shi-bai-ji-zui-jia-shi-jian-zhi-nan.html)
[解决cURL error 60: SSL certificate problem: unable to get local issuer certifica_阿里云短信ssl certificate problem: unable to get local -CSDN博客](https://blog.csdn.net/m0_61420899/article/details/122706602)
[curl - Extract CA Certs from Mozilla](https://curl.se/docs/caextract.html)

### Argument #1 ($auth_key) must be of type string, null given

Pusher\Pusher::__construct(): Argument #1 ($auth_key) must be of type string, null given

```
 Pusher\Pusher::__construct(): Argument #1 ($auth_key) must be of type string, null given, called in D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend\vendor\laravel\framework\src\Illuminate\Broadcasting\BroadcastManager.php on line 302

  at D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend\vendor\pusher\pusher-php-server\src\Pusher.php:63
     59▕      * @param ClientInterface|null $client [optional] - a Guzzle client to use for all HTTP requests
     60▕      *
     61▕      * @throws PusherException Throws exception if any required dependencies are missing
     62▕      */
  ➜  63▕     public function __construct(string $auth_key, string $secret, string $app_id, array $options = [], ClientInterface $client = null)
     64▕     {
     65▕         $this->check_compatibility();
     66▕
     67▕         $useTLS = true;

  1   D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend\vendor\laravel\framework\src\Illuminate\Broadcasting\BroadcastManager.php:302
      Pusher\Pusher::__construct(["mt1"])

  2   D:\03Coding\02Vue\vue3-pinia-and-laravel-9-blog-app\backend\vendor\laravel\framework\src\Illuminate\Broadcasting\BroadcastManager.php:284
      Illuminate\Broadcasting\BroadcastManager::pusher()
```

其实问题提示的很明显：`Pusher\Pusher::__construct(): Argument #1 ($auth_key) must be of type string, null given`，即 Pusher 类构造函数中的 `$auth_key` 必须是字符串类型，但是被传递了一个 NULL 过去。

问题在于我不知道这个 Pusher 到底是什么东西，`$auth_key` 又是什么东西。

所幸找到了 [Error Installing Composer Dependencies in Laragon: Pusher Auth Key Must be a String](https://devcodef1.com/news/1147459/laragon-composer-error-with-pusher-auth-key) 这篇博客，了解到 Pusher 其实是一个消息推送的一个包，`$auth_id` 其实是它的一个配置项。

在这篇 [实时通信 | pusher 入门教程（一） - Tinywan - 博客园](https://www.cnblogs.com/tinywan/p/15854177.html) 文章中了解到 pusher 的配置，并在 [Keys - goodly-spring-417 - Channels - Pusher](https://dashboard.pusher.com/apps/1914403/keys) 中生成了配置：

```
app_id = "1**3"
key = "f4c6**44"
secret = "44**d6"
cluster = "a**"
```

我把这些配置复制到了 `.env.example` 中，还是不行，后面在这篇 [Laravel 配置：环境变量 .env | Laravel China 社区](https://learnku.com/laravel/wikis/26072) 文章中了解到应用程序不会读取此文件，所以复制了一份，并改名为 `.env`，修改之后执行 `php artisan tinker`，提示 OK

> [!note] 参考资料
> [Error Installing Composer Dependencies in Laragon: Pusher Auth Key Must be a String](https://devcodef1.com/news/1147459/laragon-composer-error-with-pusher-auth-key)
> [Welcome to Pusher - Pusher](https://dashboard.pusher.com/)
> [广播系统 | 继续深入 |《Laravel 10 中文文档 10.x》| Laravel China 社区](https://learnku.com/docs/laravel/10.x/broadcasting/14860#introduction)
> [Laravel 配置：环境变量 .env | Laravel China 社区](https://learnku.com/laravel/wikis/26072)

### Access-Control-Allow-Origin

```
Access to XMLHttpRequest at 'http://127.0.0.1:8000/api/auth/register' from origin 'http://localhost:5173' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

[跨域请求问题 | Laravel | Laravel China 社区 (learnku.com)](https://learnku.com/laravel/t/76866)

[什么是跨域以及如何解决？通俗易懂带你彻底搞定_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV12U4y1f7Qi/?spm_id_from=333.337.search-card.all.click&vd_source=081641abeed94aff322f0473e2c1773d)

同源策略：协议、域名、端口都相同就是同源

Vue：http://127.0.0.1:8000
Laravel：http://localhost:5173

CORS：Cross Origin Resource Sharing 跨域资源共享

[前后端分离项目部署 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/600667303)

[Nginx转发解决前后端分离项目跨域请求（超详细）_nginx转发解决跨域-CSDN博客](https://blog.csdn.net/qq_39187538/article/details/122616696)

[laravel+vue前后端分离之服务器端配置 | Laravel China 社区 (learnku.com)](https://learnku.com/articles/53348)

[config/cors.php 机翻 | Laravel China 社区 (learnku.com)](https://learnku.com/articles/75727)

[Laravel 10 CORS Example: How to Enable CORS in Laravel? - positronX.io](https://www.positronx.io/how-to-enable-cors-in-laravel/)

费劲九牛二虎之力总算把这个问题解决了，真的是离谱到家了，在 `cors.php` 文件中的 allowed_origins 数组中添加 `http://localhost:5173` 后就解决了这个跨域的问题：

```PHP
<?php

...
    'allowed_origins' => [

        'http://localhost:8080',

        'http://localhost:8081',

        'http://localhost:8082',

        'http://127.0.0.1:5173',

        'http://localhost:5173' // 添加这一行后就解决了这个问题

    ],
...
```

我也是抱着试一试的心态去添加的，没想到竟然解决了，我还想着先把 nginx 搞懂来再来解决这个跨域的问题，实际上不是 nginx 的问题。

报错其实提示的很明显：`Access to XMLHttpRequest at 'http://127.0.0.1:8000/api/auth/register' from origin 'http://localhost:5173' has been blocked by CORS policy`，但是我一直以为 `http://localhost:5173` 等同于 `http://127.0.0.1:5173`，实际上是不同的，所以一直提示这个问题。

### No application encryption key has been specified

[Fix "No application encryption key has been specified." in Laravel](https://benjamincrozat.com/laravel-no-application-key-specified)