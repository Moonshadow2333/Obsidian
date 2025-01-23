---
aliases:
  - js
date: 2025-01-23
---

# Promise 对象

**`Promise`** 对象表示异步操作最终的完成（或失败）以及其结果值。

## 为什么要用 Promise

我们知道 js 执行的时候，一次只能执行一个任务，它会阻塞其他任务。由于这个缺陷导致 js 的所有网络操作，浏览器事件，都必须是异步执行。异步执行可以使用回调函数执行。

## 使用场景

- 定时器
- 接口调用
- 事件函数

### 定时器

在固定时间触发某个回调函数。

### 接口调用

对于 ajax 网络请求就没有这么简单了，可能有多个网络请求是关联的：

- 先执行某个请求返回结果后
- 第一个返回结果作为第二个请求的参数，调用第二个网络请求。

如此，如果业务复杂，网络请求太多时，回调也很多，容易出现回调地狱。所以 Promise 出现了，专门解决异步回调地狱问题。

# 语法

## 参数

下列用到的所有定时器模拟我们的 ajax 请求。

Promise 实例化的时候，传入的参数是一个函数，函数中接收两个参数：

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('123')
    }, 1000)
   }).then(res => {
    console.log(res)
   })
```

**传入的 resolve 和 reject 本身都是函数**。其作用分别为：

- resolve 函数把 Promise 的状态从进行中变为成功状态。
- reject 函数把 Promise 的状态从进行中变为拒绝状态。

## 三种状态

- pending ：进行中，表示 Promise 还在执行阶段，没有执行完成。
- fulfilled：成功状态，表示 Promise 成功执行完成。
- rejected：拒绝状态，表示 Promise 执行被拒绝，也就是失败。

Promise 的状态，只可能是其中一种状态，从进行中变为成功或失败状态之后，状态就固定了，不会再发生改变。

## Promise.then

执行 resolve 时，Promise 状态变为 fulfilled ，会执行 .then 方法。then 方法接收的参数也是一个函数，函数中携带一个参数，该参数是 resolve(res) 返回的数据。

```js
const p = new Promise((resolve,reject)=>{
setTimeout(()=>{
 resolve('哎呦喂')
 },1000)
}).then(res=>{
 console.log(res) //1秒后打印哎呦喂
})
```

## Promise.catch

执行 reject 时，Promise 状态从 pending 变为 rejected，会执行 catch 方法，catch 方法接收的也是一个函数，函数中携带一个参数，该参数为 reject(err) 返回的数据。

```js
const p = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  reject('error message')
  },1000)
 }).then(res=>{
  console.log(res)//不执行
 }).catch(err=>{
  console.log('err',err)//1秒后打印 error message
})
```

## 链式调用

制作一个模拟网络请求：

- 第一次返回 a，
- 修改返回的结果为 aa，作为第二次网络请求返回的结果。
- 修改结果为 aaa，作为第三次返回结果。

```js
const pp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  resolve('a')
 },1000)
}).then(res=>{
 console.log('res1',res) //1秒后打印 a
 return new Promise((resolve,reject)=>{
  setTimeout(()=>{
   resolve(res+'a')
   },1000)
 })
}).then(res=>{
  console.log('res',res) //2秒后打印 aa
  return new Promise((resolve,reject)=>{
   setTimeout(()=>{
    resolve(res+'a')
    },1000)
  })
 }).then(res=>{
  console.log('res3',res) //3秒后打印 aaa
})
```

这种场景其实就是接口的多层嵌套使用，Promise 可以把多层嵌套按照线性的方式进行书写，非常优雅。我们把 Promise 的多层嵌套调用就叫做链式调用。

上述实例，有三层嵌套就 new 了 3 个Promise，代码写得比较多，我们看看在实现功能的前提下如何能够简化。

## 嵌套使用的简写

promise传入的函数参数reject是一个非必传的参数，如果不需要处理失败时的结果时，我们可以省略掉 reject 。代码如下：

```js
const ppp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  resolve('a')
  },1000)
 }).then(res=>{
  console.log('res1',res)
  return new Promise(resolve=>resolve(res+'a'))
}).then(res=>{
 console.log('res',res)
 return new Promise(resolve=>resolve(res+'a'))
}).then(res=>{
 console.log('res3',res)
})
```

Promise 嵌套使用时，内层的 Promise 可以省略不写，所以我们可以直接把 Promise 相关的去掉，直接返回，代码如下：

```js
const pppp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  resolve('a')
 },1000)
}).then(res=>{
 return  res+'a'
}).then(res=>{
 return res+'a'
}).then(res=>{
 console.log('res3',res)
})
```

有的同学就在想，怎么都是成功状态的举例和简写，我们的失败状态catch可以简写吗？

答案是肯定的，我们简化为2层嵌套，与上述功能一致。

```js
const ppppp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  reject('a')
 },1000)
}).catch(err=>{
 return new Promise((resolve,reject)=>{
  setTimeout(()=>{
   reject(err+'a')
  },1000)
 })
}).catch(err=>{
 console.log('err',err)
})

//简写1
const pppppp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  reject('a')
  },1000)
 }).catch(err=>{
  return new Promise((resolve,reject)=>reject(err+'a'))
 }).catch(err=>{
  console.log('err',err)
 })

//简写2
const ppppppp = new Promise((resolve,reject)=>{
 setTimeout(()=>{
  reject('a')
  },1000)
 }).catch(err=>{
  throw err+'a'
 }).catch(err=>{
  console.log('err',err)
})
```

注意：失败简写省略掉Promise时，使用的 throw 抛出异常。

## Promise 方法

- all 方法：可以并行执行异步操作的能力，在所有异步操作完成之后，统一返回所有结果
- race 方法：返回执行最快的那个 Promise 结果

### all 方法

```js
Promise.all([
 new Promise(resolve=>resolve('a')),
 new Promise(resolve=>resolve('b')),
]).then(res=>{
 console.log('all',res)//【'a' , 'b'】
 })
```

### race 方法

```js
Promise.race([
 new Promise(resolve=>
  setTimeout(()=>{
   resolve('a')
   },100)
  ),
 new Promise(resolve=>
  setTimeout(()=>{
   resolve('a')
   },200)
  ),
 ]).then(res=>{
  console.log('race',res) // 返回 a
})
```

# 参考资料

> [!note]
> [Promise - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)
> [大白话透彻讲解 Promise 的使用，读完你就懂了我们知道 js 执行的时候，一次只能执行一个任务，它会阻塞其他任务。 - 掘金](https://juejin.cn/post/7011755708496478215) ⭐⭐⭐⭐⭐