# yield

- 生成器就是一种迭代器，可以使用for进行迭代。
- 生成器函数最大的特点是可以接受外部传入的一个变量，并根据变量内容计算结果后返回。   
- 这一切都是靠生成器内部的send()函数实现的。

```python
def gen():
    value=0
    while True:
        receive=yield value
        if receive=='e':
            break
        value = 'got: %s' % receive

g=gen()
print(g.send(None))    
print(g.send('hello'))
print(g.send(123456))
print(g.send('e'))
```

 `receive=yield value` 包含了3个步骤： 

1. 向函数外抛出（返回）value 
2. 暂停(pause)，等待next()或send()恢复 
3. 赋值receive=MockGetValue() 。 这个MockGetValue()是假想函数，用来接收send()发送进来的值

## 用法

```python
# coding: utf8

# 生成器
def gen(n):
    for i in range(n):
        yield i

g = gen(5)      # 创建一个生成器
print(g)        # <generator object gen at 0x10bb46f50>
print(type(g))  # <type 'generator'>

# 迭代生成器中的数据
for i in g:
    print(i)

# Output:
# 0 1 2 3 4
```

注意，在这个例子中，当我们执行 `g = gen(5)` 时，`gen` 中的代码其实并没有执行，此时我们只是创建了一个「生成器对象」，它的类型是 `generator`。

然后，当我们执行 `for i in g`，每执行一次循环，就会执行到 `yield` 处，返回一次 `yield` 后面的值。

这个迭代过程是和迭代器最大的区别。

换句话说，如果我们想输出 5 个元素，在创建生成器时，这个 5 个元素其实还并没有产生，什么时候产生呢？只有在执行 `for` 循环遇到 `yield` 时，才会依次生成每个元素。

此外，生成器除了和迭代器一样实现迭代数据之外，还包含了其他方法：

- `generator.__next__()`：执行 `for` 时调用此方法，每次执行到 `yield` 就会停止，然后返回 `yield` 后面的值，如果没有数据可迭代，抛出 `StopIterator` 异常，`for` 循环结束
- `generator.send(value)`：外部传入一个值到生成器内部，改变 `yield` 前面的值
- `generator.throw(type[, value[, traceback]])`：外部向生成器抛出一个异常
- `generator.close()`：关闭生成器

通过使用生成器的这些方法，我们可以完成很多有意思的功能。

# yield from

- yield from iterable本质上等于for item in iterable: yield item的缩写版
- 如果生成器函数需要产出另一个生成器生成的值，传统的解决方法是使用嵌套的for循环：

# 参考资料

> [!ifo] 参考资料
>  - [理解Python协程:从yield/send到yield from再到async/await - 风声风语 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhaohuanhuan/p/10489759.html)|very important
> - [深入理解Python 中的 yield from语法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/267966140#:~:text=%E5%BD%93%E8%BF%AD%E4%BB%A3%E5%99%A8%E7%BB%93%E6%9D%9F)
> - [Python yield from 用法详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/87da832730f5)
> - [Python进阶——如何正确使用yield？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/321302488#:~:text=%E5%88%A9%E7%94%A8%20yie)
