
今天要讲的HTTP请求头的Content-Type字段，就是在curl发送请求的时候需要指定以何种方式来请求数据，按照postman的POST方法的分类，常用的有3类：

1、form-data 就是 multipart/form-data 使用表单的方式来发送数据，**是curl采用的默认发送方式**。

2、x-www-form-urlencoded 就是 application/x-www-form-urlencoded 把请求的内容转变成url参数的形式进行发送，如：s1=red&s2=blue，这是标准的编码格式，但在curl中却不是默认的发送方式。

3、raw（text/plain application/json text/xml等） 是以纯文本的方式发送数据，可以选择json、xml等格式

## form-data

D:\phpstudy_pro\WWW\Curl\Formdata\curl_form_data.php
```PHP
<?php

  

$url = 'http://localhost/Curl/Formdata/hello.php';

// 格式化multipart/form-data内容

$data = array(

    'field1' => 'value1',

    'field2' => 'value2'

    // 'file' => new CURLFile('/path/to/file')

);

$result = curlPostFormData($url, $data);

  

var_dump($result);

function curlPostFormData($url, array $data) {

    // 初始化cURL

    $ch = curl_init();

  

    // 设置URL和其他选项

    curl_setopt($ch, CURLOPT_URL, $url);

    curl_setopt($ch, CURLOPT_POST, 1);

    curl_setopt($ch, CURLOPT_POSTFIELDS, $data);

    curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);



    // 执行请求并处理响应

    $result = curl_exec($ch);

  

    // 关闭cURL句柄

    curl_close($ch);

    return $result;

}
```
D:\phpstudy_pro\WWW\Curl\Formdata\hello.php
```PHP
<?php

$params = $_POST;

echo json_encode($params);
```

浏览器访问：http://localhost//Curl/Formdata/curl_form_data.php
结果如下：
```
D:\phpstudy_pro\WWW\Curl\Formdata\curl_form_data.php:12: string(37) "{"field1":"value1","field2":"value2"}"
```


## 参考

[PHP的curl有三种请求数据的方式你需要知道raw、form-data、x-www-form-urlencoded - 爱家家的卡卡 - 博客园 (cnblogs.com)](https://www.cnblogs.com/kaka0318/p/15424223.html)