# async

事件循环机制分为以下几步骤:

1. 创建一个事件循环
2. 将异步函数加入事件队列
3. 执行事件队列, 直到最晚的一个事件被处理完毕后结束
4. 最后建议用 close() 方法关闭事件循环, 以彻底清理 loop 对象防止误用

# 参考资料

> [!info] 参考资料
> [Python Async/Await入门指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/27258289#:~:text=Python)
> [轻松理解 Python 中的 async await 概念 - 狂客 - 博客园 (cnblogs.com)](https://www.cnblogs.com/kuangke/p/14702545.html#:~:text=%E8%BF%99%E4%B8%AA%20awa) 五颗星
> [(71 封私信 / 80 条消息) python中的cls到底指的是什么，与self有什么区别? - 知乎 (zhihu.com)](https://www.zhihu.com/question/49660420#:~:text=%E4%B8%80%E8%88%AC%E6%9D%A5%E8%AF%B4%EF%BC%8C%E8%A6%81)