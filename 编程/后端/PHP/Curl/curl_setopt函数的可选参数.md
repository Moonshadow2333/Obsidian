
## CURLOPT_RETURNTRANSFER

使用PHP curl获取页面内容或提交数据，有时候希望返回的内容作为变量储存，而不是直接输出。这个时候就必需设置curl的CURLOPT_RETURNTRANSFER选项为1或true。

[PHP curl获取页面内容，不直接输出到页面，CURLOPT_RETURNTRANSFER参数设置 - 52php - 博客园 (cnblogs.com)](https://www.cnblogs.com/52php/p/5677692.html)

## **CURLOPT_POSTFIELDS**

全部数据使用HTTP协议中的"POST"操作来发送。要发送文件，在文件名前面加上@前缀并使用完整路径。这个参数可以通过urlencoded后的字符串类似'para1=val1&para2=val2&...'或使用一个以字段名为键值，字段数据为值的数组。**如果value是一个数组，Content-Type头将会被设置成multipart/form-data**。