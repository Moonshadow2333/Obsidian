---
aliases:
  - Vue
date: 2025-04-20
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

# 前言

上周用 Vue 写表单页面的时候，我想实现表单验证失败或者请求失败时页面需要提示失败信息，即网络请求失败的异常和表单验证的异常用同一个 catch 捕获，但是写的代码比较混乱，可读性差，也没实现最终的效果，就提交给了 AI，让它帮忙[[代码优化|优化]]。它指出了这段代码的问题：[[Async await]] 和 [[Promise]] 混用，即对这两个工具的理解出现了偏差。

# 混用代码

```js
const submitForm = async () => {
        try {
            await formRef.value.validate().then(() => {
                axios.post('http://127.0.0.1:5000/api/user', form, {
                    headers: {
                        'Content-Type': 'application/json'
                    }
                }).then(response => {
                    if (response.data.status === 'success') {
                        setTimeout(() => {
                            router.push('/about')
                        }, 3000)
                    }
                }).catch(error => {
                    throw new Error(error.response.data.error)
                })
            }).catch((error) => {
                console.log(error)
            })
        } catch (error) {
            console.log(error)
            
            ElMessage.error('验证失败：' + error.message)
        }
    }
```

在 JavaScript 的异步编程中，`async/await` 和 `Promise 链（.then()/.catch()）` 是处理异步操作的两种不同语法，混合使用会导致 **代码结构混乱** 和 **错误处理路径不明确**。以下是具体分析：

---

### 为什么会出现混用？

开发者通常因为以下原因混合使用两种语法：
1. **对异步机制理解不深**：不了解 `async/await` 本质上是 Promise 的语法糖。
2. **渐进式改造代码**：在改造旧代码时，部分保留 Promise 链，部分改用 `async/await`。
3. **错误处理困惑**：试图在局部使用 `.catch()` 处理特定错误，但未处理好错误冒泡。

---

### 混用的具体位置（以你的代码为例）

```javascript
const submitForm = async () => {
  try {
    // 混用点：在 async 函数内部使用 await + .then()
    await formRef.value.validate().then(() => {
      axios.post(...).then(response => {  // 嵌套的 Promise 链
        // ...
      }).catch(error => {  // 内部 catch
        throw new Error(error.response.data.error)
      })
    }).catch((error) => {  // 外部 catch
      console.log(error)
    })
  } catch (error) {  // 最外层 catch
    ElMessage.error('验证失败：' + error.message)
  }
}
```

#### 混用点详解：
1. **`await` 与 `.then()` 混合**  
   `formRef.value.validate()` 本身返回 Promise，通过 `await` 等待其完成。但紧接着又使用 `.then()` 处理结果，导致：
   - **冗余等待**：`await` 已经等待 Promise 完成，后续 `.then()` 实际是同步代码。
   - **破坏线性逻辑**：`async/await` 的优势在于用同步写法处理异步，嵌套 `.then()` 破坏了可读性。

2. **多层 `.catch()` 嵌套**  
   内部的 `.catch()` 试图处理 `axios.post` 的错误，但抛出的错误会被外层的 `.catch()` 捕获，最终又被最外层的 `try/catch` 捕获，导致：
   - **错误处理路径混乱**：同一个错误可能被多次处理。
   - **错误信息丢失**：内部 `throw` 的错误可能被外层捕获后无法区分来源。

3. **错误冒泡未处理**  
   内部 `.catch()` 使用 `throw` 重新抛出错误，但外层的 `.catch()` 仅打印日志，未继续抛出，导致最外层的 `try/catch` 无法捕获该错误。

---

### 为什么说这是问题？

#### 1. **代码结构混乱**
- **嵌套层次深**：`await` + `.then()` 形成不必要的嵌套，破坏代码的线性可读性。
- **逻辑分散**：错误处理分散在多个 `.catch()` 和 `try/catch` 中，难以追踪执行路径。

#### 2. **错误处理不可控**
- **错误被静默吞噬**：外层 `.catch()` 未重新抛出错误时，最外层 `try/catch` 无法捕获。
- **错误类型混淆**：多个 `.catch()` 可能处理同一错误，导致重复提示或漏处理。

#### 3. **性能浪费**
- **冗余等待**：`await` 已经等待 Promise 解析，后续 `.then()` 增加不必要的微任务。

---

### 正确做法：统一使用 `async/await`

```javascript
const submitForm = async () => {
  try {
    // 1. 用 await 替代 .then()
    await formRef.value.validate();

    // 2. 直接 await 请求结果
    const response = await axios.post('http://127.0.0.1:5000/api/user', form, {
      headers: { 'Content-Type': 'application/json' }
    });

    // 3. 统一用 try/catch 处理错误
    if (response.data.status === 'success') {
      router.push('/about');
    }
  } catch (error) {
    // 4. 集中处理所有错误
    let message = '请求失败';
    if (error.response) {
      message = error.response.data.error || message;
    } else if (error.message.includes('validate')) {
      message = '表单验证失败';
    }
    ElMessage.error(message);
  }
};
```

---

### 关键改进点

| 问题                 | 原代码                     | 优化后代码               | 优势                          |
|----------------------|--------------------------|------------------------|-------------------------------|
| 嵌套结构             | `await` + `.then()` 嵌套 | 纯 `await` 线性执行     | 代码可读性提升                |
| 错误处理分散         | 多层 `.catch()`          | 单一 `try/catch` 块     | 错误处理集中可控              |
| 错误信息丢失         | 内部 `throw` 未传递      | 统一解析错误对象        | 精准显示错误原因              |
| 不必要的微任务      | 多次 `.then()` 链        | 直接 `await` 结果       | 减少事件循环负担              |

---

### 总结

- **避免混用**：在 `async` 函数中，优先使用 `await` 替代 `.then()`。
- **统一错误处理**：用 `try/catch` 替代分散的 `.catch()`，通过 `error` 对象区分错误类型。
- **保持代码线性**：利用 `async/await` 的同步写法优势，避免嵌套回调。

通过统一异步处理方式，代码可维护性和可读性会显著提升！