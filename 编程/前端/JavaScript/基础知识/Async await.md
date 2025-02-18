---
aliases:
  - js
date: 2025-01-23
---

# 什么是 Async await

`async function` 声明创建一个 [`AsyncFunction`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/AsyncFunction) 对象。每次调用异步函数时，都会返回一个新的 [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 对象，该对象将会被解决为异步函数的返回值，或者被拒绝为异步函数中未捕获的异常。

async 是一个通过异步执行并隐式返回 [[Promise]] 作为结果的函数

关键字：异步执行，隐式返回

# 为什么要用 Async await

[[Promise]] 的编程模型虽然解决了回调地狱的问题，但是语义方面依然存在缺陷，代码中充斥者大量的 then 函数，这就是 Async await 的原因。Async await 让代码更少，更简洁。

It’s just a more elegant syntax of getting the promise result than promise.then. And, it’s easier to read and write.

# Async 函数

在一个普通函数的前面加上 async 关键字：

```js
async function f() {
  return 1;
}
```

The word “async” before a function means one simple thing: a function always returns a promise. Other values are wrapped in a resolved promise automatically.

加了 `async` 关键字的函数永远返回一个 `promise`，其他值会自动包裹在一个 resolved 的 promise 里

例如，上面的例子会返回一个值为 1 的 resolved promise：

```js
async function f() {
       return 1 
   }
f().then(res => {
	console.log(res) // 1
})
```

我们也能显示地返回一个 promise，得到的结果是一样的：

```js
async function f() {
       return Promise.resolve(1)
   }
f().then(res => {
	console.log(res) // 1
})
```

# Await

语法：

```js
// works only inside async functions 
let` value `=` `await` promise`;
```

关键字 await 使 JavaScript 等待，直到该 promise 建立并返回其结果。

例子：

```js
async function f() {
	let promise = new Promise((resolve, reject) => {
		setTimeout(() => {
			resolve('Done')
		}, 1000)
	})
	let result = await promise // wait until the promise resolves (*)
	console.log(result) // Done
}
f()
```

The function execution “pauses” at the line `(*)` and resumes when the promise settles, with `result` becoming its result. So the code above shows “done!” in one second.

- 函数执行到 `(*)` 行时暂停
- 当 promise settles 时，函数恢复
- 所以上面的代码在一秒后打印了 Done

await 挂起函数 -> promise 的状态变更 -> 恢复函数

说到暂停和恢复，很容易联想到 python 中的 [[00yield|yield]]

# 链式调用

```js
async function showAvatar() {
	let response = new Promise((resolve, reject) => {
		setTimeout(() => {
			resolve({'name':'Violet', 'age':18})
		}, 1000)
	})
	let user = await response 
	let githubResponse = new Promise((resolve, reject) => {
		console.log('通过 username 查询')
		setTimeout(() => {
			resolve({'name':user.name, 'age':user.age, 'avatar_url':'Violet_20250123232915.png'})
		}, 2000)
	})
	let info = await githubResponse
	console.log(info.avatar_url) //Violet_20250123232915.png
}
```

简洁易读

# 异常处理

- If a promise resolves normally, then await promise returns the result. 
- But in the case of a rejection, it throws the error, just as if there were a throw statement at that line.

## reject

This code:

```js
async function f() {
  await Promise.reject(new Error("Whoops!"));
}
```

## 错误处理

和上面一致：

```js
async function f() {
  throw new Error("Whoops!");
}
```

In real situations, the promise may take some time before it rejects. In that case there will be a delay before `await` throws an error.

We can catch that error using `try..catch`, the same way as a regular `throw`:

```js
async function f() {

  try {
    let response = await fetch('http://no-such-url');
  } catch(err) {
    alert(err); // TypeError: failed to fetch
  }
}

f();
```

In the case of an error, the control jumps to the `catch` block. We can also wrap multiple lines:

```js
async function f() {

  try {
    let response = await fetch('/no-user-here');
    let user = await response.json();
  } catch(err) {
    // catches errors both in fetch and response.json
    alert(err);
  }
}

f();
```


If we don’t have `try..catch`, then the promise generated by the call of the async function `f()` becomes rejected. We can append `.catch` to handle it:

```js
async function f() {
  let response = await fetch('http://no-such-url');
}

// f() becomes a rejected promise
f().catch(alert); // TypeError: failed to fetch // (*)
```

# 参考资料

> [!note]
> [async function - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/async_function)
> [理解异步函数async和await的用法_async await用法-CSDN博客](https://blog.csdn.net/weixin_45811256/article/details/123638582)
> [Async/await](https://javascript.info/async-await)