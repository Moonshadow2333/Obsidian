## Access-Control-Allow-Origin

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