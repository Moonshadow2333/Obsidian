---
aliases: 
date: 2025-04-22
---

# 目录

```dataviewjs
const startHeadinglevel = 2;
const file = app.workspace.getActiveFile();
const { headings } = app.metadataCache.getFileCache(file);
 
// 全列表的形式
const raws = headings.filter(row => row.heading != "目录").map( p => {
    let repeatCount = Math.max((p.level - startHeadinglevel) * 4, 0);
    let spacesPrefix = ' '.repeat( repeatCount + 4 );
    let listSign = repeatCount > 0 ? '- ' : '';
    let linkText = `[[#${p.heading}]]`;
    let headingList = (p.level < startHeadinglevel) ? `- ${linkText}` : `${spacesPrefix}- ${linkText}`;
    return headingList;
  }
)
 
let result = raws.join('\n');
// 添加行距
dv.container.style.lineHeight = "1.5em";
dv.paragraph(result)
```



手写一个简化版 `Promise` 的核心实现，包含基础状态管理、`then` 方法和异步支持：

```javascript
class MyPromise {
  constructor(executor) {
    this.state = 'pending'; // 状态：pending/fulfilled/rejected
    this.value = undefined; // 成功值
    this.reason = undefined; // 失败原因
    this.onFulfilledCallbacks = []; // 成功回调队列
    this.onRejectedCallbacks = []; // 失败回调队列

    const resolve = (value) => {
      if (this.state === 'pending') {
        this.state = 'fulfilled';
        this.value = value;
        // 执行所有成功回调（支持异步）
        this.onFulfilledCallbacks.forEach(fn => fn());
      }
    };

    const reject = (reason) => {
      if (this.state === 'pending') {
        this.state = 'rejected';
        this.reason = reason;
        // 执行所有失败回调（支持异步）
        this.onRejectedCallbacks.forEach(fn => fn());
      }
    };

    try {
      executor(resolve, reject); // 立即执行传入的函数
    } catch (err) {
      reject(err); // 捕获同步错误
    }
  }

  then(onFulfilled, onRejected) {
    // 值穿透（如果then参数不是函数，直接透传value）
    onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : v => v;
    onRejected = typeof onRejected === 'function' ? onRejected : err => { throw err; };

    const promise2 = new MyPromise((resolve, reject) => {
      const handleFulfilled = () => {
        setTimeout(() => { // 模拟微任务（此处用宏任务简化实现）
          try {
            const x = onFulfilled(this.value);
            resolve(x); // 链式调用传递结果
          } catch (err) {
            reject(err);
          }
        }, 0);
      };

      const handleRejected = () => {
        setTimeout(() => {
          try {
            const x = onRejected(this.reason);
            resolve(x); // 错误被处理后，后续链继续走成功回调
          } catch (err) {
            reject(err);
          }
        }, 0);
      };

      if (this.state === 'fulfilled') {
        handleFulfilled();
      } else if (this.state === 'rejected') {
        handleRejected();
      } else { // pending状态时，将回调存入队列
        this.onFulfilledCallbacks.push(handleFulfilled);
        this.onRejectedCallbacks.push(handleRejected);
      }
    });

    return promise2; // 实现链式调用
  }

  catch(onRejected) {
    return this.then(null, onRejected);
  }
}
```

---

### 使用示例
```javascript
// 测试基础功能
const p = new MyPromise((resolve, reject) => {
  setTimeout(() => resolve('成功'), 1000);
});

p.then(res => {
  console.log(res); // 1秒后输出"成功"
  return '新的值';
}).then(res => {
  console.log(res); // 输出"新的值"
});
```

---

### 核心实现要点
1. **三种状态管理**  
   `pending`、`fulfilled`、`rejected` 状态不可逆，确保只能触发一次

2. **异步支持**  
   用回调队列 (`onFulfilledCallbacks`/`onRejectedCallbacks`) 存储异步回调

3. **链式调用**  
   `then` 方法返回新 Promise，通过 `resolve(x)` 传递结果

4. **错误处理**  
   - 构造函数内 `try/catch` 捕获同步错误  
   - 回调执行时的 `try/catch` 包裹

5. **值穿透**  
   处理 `then` 参数非函数时的默认行为

---

### 完整版需补充
- `Promise.resolve`/`Promise.reject` 静态方法  
- `Promise.all`/`Promise.race` 等扩展方法  
- 更严谨的循环引用检测  
- 真实的微任务队列实现（可用 `queueMicrotask`）

# 核心原理

Promise 的核心原理是通过**状态机 + 回调队列 + 链式调用**实现异步操作的统一管理。以下是其核心原理的拆解：

---

### 1. **状态机机制**  
Promise 是一个**状态不可逆**的有限状态机，包含三种状态：
- **`pending`（等待中）**：初始状态，未完成或未拒绝。
- **`fulfilled`（已成功）**：操作成功完成，有确定的值。
- **`rejected`（已失败）**：操作失败，有拒绝原因。

**关键规则**：  
- 状态一旦变为 `fulfilled` 或 `rejected`，**不可再改变**（例如：不能从成功变回失败）。
- 状态改变后会触发对应的回调队列。

---

### 2. **回调队列管理**  
当 Promise 处于 `pending` 状态时，通过 `then` 或 `catch` 注册的回调会被**存入队列**，直到状态改变后依次执行。

```javascript
// 示例：回调队列的触发
const p = new Promise((resolve) => {
  setTimeout(() => resolve("成功"), 1000); // 异步操作
});

p.then((res) => console.log(res)); // 回调存入队列，1秒后状态变为fulfilled时执行
```

---

### 3. **链式调用（Chaining）**  
Promise 的 `then` 方法返回**新的 Promise**，形成链式调用。  
- **返回值处理**：  
  - 如果回调返回普通值（非 Promise），新 Promise 直接以该值 `resolve`。  
  - 如果回调返回 Promise，则等待其状态改变后再传递结果。  
- **错误冒泡**：链式调用中，若某一环发生错误，会跳过后续的 `then`，直接触发最近的 `catch`。

```javascript
// 链式调用示例
new Promise((resolve) => resolve(1))
  .then((res) => res * 2)         // 返回 2
  .then((res) => Promise.resolve(res + 3)) // 返回新 Promise，最终值 5
  .then(console.log)              // 输出 5
  .catch((err) => console.error(err)); // 统一捕获错误
```

---

### 4. **错误冒泡与统一捕获**  
- **同步错误**：在 `executor` 或 `then` 回调中抛出同步错误时，Promise 自动捕获并转为 `rejected` 状态。  
- **异步错误**：需手动调用 `reject` 或抛出错误（例如在 `setTimeout` 中）。

```javascript
// 错误捕获示例
new Promise((resolve, reject) => {
  throw new Error("同步错误"); // 自动被捕获，状态变为rejected
}).catch(console.error); // 输出错误

new Promise((resolve, reject) => {
  setTimeout(() => {
    try {
      throw new Error("异步错误");
    } catch (err) {
      reject(err); // 需手动调用reject
    }
  }, 1000);
}).catch(console.error);
```

---

### 5. **值穿透（Value Propagation）**  
当 `then` 的参数不是函数时，Promise 会直接将上一个结果**透传**给后续链式调用。

```javascript
// 值穿透示例
Promise.resolve("hello")
  .then(null) // 参数不是函数，透传"hello"
  .then(console.log); // 输出 "hello"
```

---

### 6. **微任务（Microtask）队列**  
Promise 的回调（`then/catch/finally`）属于**微任务**，比 `setTimeout` 等宏任务优先级更高。  
- **实现方式**：浏览器用 `queueMicrotask`，Node.js 用 `process.nextTick`。  
- **效果**：确保 Promise 回调在本次事件循环末尾立即执行。

```javascript
// 微任务与宏任务执行顺序
setTimeout(() => console.log("宏任务"), 0); 

Promise.resolve()
  .then(() => console.log("微任务")); 

// 输出顺序：微任务 → 宏任务
```

---

### 核心原理总结
| 机制              | 作用                                                                 |
|-------------------|----------------------------------------------------------------------|
| 状态机            | 保证操作的原子性，状态不可逆                                         |
| 回调队列          | 管理异步回调的执行顺序                                               |
| 链式调用          | 通过返回新 Promise 实现链式操作                                       |
| 错误冒泡          | 统一错误处理，避免回调地狱                                           |
| 微任务队列        | 确保异步回调的高优先级执行                                           |

通过理解这些核心原理，可以更好地掌握 Promise 的工作机制，并应对复杂的异步编程场景。

# 技术旦老师手写 Promise 笔记

1. 在得到 Promise 时，我们使用的是 new 关键字 -- 对象
2. 在 new  Promise 时，我们需要传入一个函数，这个函数可以是空函数
	
```js
let promise = new Promise(() => {})
```

3. 这个函数一般情况下是以 resolve 和 reject 作为参数的函数

```js
let promise = new Promise((resolve, reject) => {

    setTimeout(() => {

        resolve(100)

    }, 2000)

})
```

4. 成功时，执行 resolve 函数，并且会把结果保存起来
5. 失败时，执行 reject 函数，并且抛出异常
6. resolve/reject 函数接收一个参数，后面就可以使用这个参数
7. resolve 和 reject 函数都是内置函数，resolve 方法执行之后状态变成 fulfilled，rejected 方法执行之后状态变为 reject，状态不可逆，执行 resolve/reject 时会给结果赋值
8. then 函数，接收两个参数，一个时 onFulFilled 和 onRejected
9. onFulFilled 和 onRejected 都是可选参数
10. resolve 方法先于 then 方法执行，需要保证 then 方法执行于 reslove 方法之后，回调队列，发布订阅者模型
11. 支持链式调用

---

this 指向问题
执行异常
异步


## 参考代码

```js
class MyPromise {

    static PENDING = '待定'; static FULFILLED = '成功'; static REJECTED = '拒绝';

    constructor(func) {

        this.status = MyPromise.PENDING

        this.result = null

        this.resolveCallbacks = []

        this.rejectCallbacks = []

        try {

            func(this.resolve.bind(this), this.reject.bind(this))

        } catch (error) {

            this.reject(error)

        }

    }

    resolve(result) {

        setTimeout(() => {

            if (this.status == MyPromise.PENDING) {

                this.status = MyPromise.FULFILLED

                this.result = result

                this.resolveCallbacks.forEach(callback => {

                    callback(result)

                })

            }

        })

    }

  

    reject(result) {

        setTimeout(() => {

            if (this.status == MyPromise.PENDING) {

                this.status = MyPromise.REJECTED

                this.result = result

                this.rejectCallbacks.forEach(callback => {

                    callback(result)

                })

            }

        })

    }

  

    then (onFULFILLED, onREJECTED) {

        onFULFILLED = typeof onFULFILLED == 'function' ? onFULFILLED : () => {}

        onREJECTED = typeof onREJECTED == 'function' ? onREJECTED : () => {}

        if (this.status === MyPromise.PENDING) {

            this.resolveCallbacks.push(onFULFILLED)

            this.rejectCallbacks.push(onREJECTED)

        }

        if (this.status === MyPromise.FULFILLED) {

            setTimeout(() => {

                onFULFILLED(this.result)

            })

        }

        if (this.status === MyPromise.REJECTED) {

            setTimeout(() => {

                onREJECTED(this.result)

            })

        }

    }

}

  

console.log('第一步')

let my = new MyPromise((resolve, reject) => {

    console.log('第二步')

    resolve('第2.5步')

    setTimeout(() => {

        resolve('这次一定')

        reject('这次一定')

        console.log('第四步')

    })

})

  

my.then(

    result => {console.log(result)},

    result => {console.log(result.message)}

)

console.log('第三步')
```

# 参考

[javascript - 手写一个Promise/A+,完美通过官方872个测试用例 - 进击的大前端 - SegmentFault 思否](https://segmentfault.com/a/1190000023157856)
[手写Promise核心代码 - JavaScript前端Web工程师_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1RR4y1p7my/?spm_id_from=333.1007.top_right_bar_window_history.content.click&vd_source=081641abeed94aff322f0473e2c1773d)