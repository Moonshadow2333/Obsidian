## 前言

昨天在开发导出集采订单数据，需要导出 Excel，政采系统用的是 lumen 框架，即精简版的 Laravel，很多常用的功能都没有，例如导出 Excel，所以我就想着先用 PHP 代码查出这些数据，然后输出 SQL 语句，在 Navicat 里面执行，最后导出结果即可。

以前我应该就用过这个功能的，但是一下用 TP6，一下用 Laravel，就用混淆了，找了半天才找到输出 SQL 语句的语法。。。

## 输出 SQL 语句

```
$query = \DB::table('users')->where('name', 'myname');

echo $query->toSql();
```

## 参考

[Laravel 数据库：输出 SQL 语句](https://learnku.com/laravel/wikis/27707)