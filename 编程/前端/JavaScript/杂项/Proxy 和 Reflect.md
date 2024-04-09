## 什么是 Proxy

> 一个 `Proxy` 对象包装另一个对象并拦截诸如读取/写入属性和其他操作，可以选择自行处理它们，或者透明地允许该对象处理它们。

关键字：包装、拦截、自行处理。

## Proxy 语法

```js
let proxy = new Proxy(target, handler)
```

参数：

- target：被包装的对象，可以是任何东西，包括函数；
- handler：代理配置，带有捕捉器的对象。

上文提到的捕捉器指的是拦截操作的方法，例如：

- get 捕捉器用于读取 target 属性；
- set 捕捉器用于写入 target 属性。

注意，对 proxy 进行操作，**如果在 handler 中存在相应的捕捉器，则它将运行，并且 proxy 有机会对其进行处理；否则将直接对 target 进行处理**。

例如，我们创建一个没有任何捕捉器的代理（Proxy）：

```js
let target = {};
let proxy = new Proxy(target, {}); // 空的 handler 对象

proxy.test = 5; // 写入 proxy 对象 (1)
alert(target.test); // 5，test 属性出现在了 target 中！

alert(proxy.test); // 5，我们也可以从 proxy 对象读取它 (2)

for(let key in proxy) alert(key); // test，迭代也正常工作 (3)
```

由于代理没有捕捉器，所有对 `proxy` 的操作都直接转发给了 `target`。

1. 写入操作 `proxy.test=` 会将值写入 `target`。
2. 读取操作 `proxy.test` 会从 `target` 返回对应的值。
3. 迭代 `proxy` 会从 `target` 返回对应的值。

我们可以看到，没有任何捕捉器，`proxy` 是一个 `target` 的透明包装器（wrapper）。

## 捕捉器类型

上文提到，当 `proxy` 中没有任何捕捉器时，对 `proxy` 的所有操作都会直接转发给 `target`。

如果我们想要拦截对 `proxy` 的操作，就需要在 `handler` 中添加捕捉器。

在使用捕捉器之前，我们先了解一下有多少种捕捉器以及每种捕捉器的具体功能：


| 序号 | 名称                     | 描述                                                                                          |
| ---- | ------------------------ | --------------------------------------------------------------------------------------------- |
| 1    | get                      | 读取属性                                                                                      |
| 2    | set                      | 写入属性                                                                                      |
| 3    | has                      | in 操作符                                                                                     |
| 4    | deleteProperty           | delete 操作符                                                                                 |
| 5    | apply                    | 函数调用                                                                                      |
| 6    | construct                | new 操作符                                                                                    |
| 7    | getPrototypeOf           | Object.getPrototypeOf                                                                         |
| 8    | setPrototypeOf           | Object.setPrototypeOf                                                                         |
| 9    | isExtensible             | Object.isExtensible                                                                           |
| 10   | preventExtensions        | Object.preventExtensions                                                                      |
| 11   | defineProperty           | Object.defineProperty, Object.defineProperties                                                |
| 12   | getOwnPropertyDescriptor | Object.getOwnPropertyDescriptor, for..in, Object.keys/values/entries                          |
| 13   | ownKeys                  | Object.getOwnPropertyNames, Object.getOwnPropertySymbols, for..in, Object.keys/values/entries |


## 捕捉器的实际应用

### 带有 “get” 捕捉器的默认值

前文提到，`get` 捕捉器可以拦截读取操作，语法为 `get(target, property, receiver)`，其中：

- target：被包装的对象；
- property：目标属性名；
- receiver：如果目标属性是一个 getter 访问器属性，则 `receiver` 就是本次读取属性所在的 `this` 对象。通常，这就是 `proxy` 对象本身（或者，如果我们从 proxy 继承，则是从该 proxy 继承的对象）。

在 JavaScript 中，当访问的属性不存在数组中时会得到 undefined。现在我们可以将常规数组包装到 proxy 中，并在 proxy 中使用 get 捕捉器，实现当访问不存在的属性时返回一个默认值的功能。

例子，当访问的属性不在数组中时，返回默认值 0：

```JS
let numbers = [0, 1, 2];

numbers = new Proxy(numbers, {
  get(target, prop) {
    if (prop in target) {
      return target[prop];
    } else {
      return 0; // 默认值
    }
  }
});

alert( numbers[1] ); // 1
alert( numbers[123] ); // 0（没有这个数组项）
```

### 使用 “set” 捕捉器进行验证

前文提到，set 捕捉器可以拦截写入操作，语法为 `set(target, property, value, receiver)`，其中：

- target：被包装的对象；
- property：目标属性名称；
- value：目标属性的值；
- receiver：与 get 捕捉器类似，仅与 setter 访问器属性相关。

注意：**如果写入操作（setting）成功，`set` 捕捉器应该返回 `true`，否则返回 `false`（触发 `TypeError`）**。

例子，在写入数据之前校验写入数据的数据类型：

```JS
let numbers = [];

numbers = new Proxy(numbers, { // (*)
  set(target, prop, val) { // 拦截写入属性操作
    if (typeof val == 'number') {
      target[prop] = val;
      return true;
    } else {
      return false;
    }
  }
});

numbers.push(1); // 添加成功
numbers.push(2); // 添加成功
alert("Length is: " + numbers.length); // 2

numbers.push("test"); // TypeError（proxy 的 'set' 返回 false）

alert("This line is never reached (error in the line above)");
```

### 使用 “ownKeys” 和 “getOwnPropertyDescriptor” 进行迭代

`Object.keys`，`for..in` 循环和大多数其他遍历对象属性的方法都使用内部方法 `[[OwnPropertyKeys]]`（由 `ownKeys` 捕捉器拦截) 来获取属性列表。

这些方法在细节上有所不同：

- `Object.getOwnPropertyNames(obj)` 返回非 symbol 键。
- `Object.getOwnPropertySymbols(obj)` 返回 symbol 键。
- `Object.keys/values()` 返回带有 `enumerable` 标志的非 symbol 键/值（属性标志在 [属性标志和属性描述符](https://zh.javascript.info/property-descriptors) 一章有详细讲解)。
- `for..in` 循环遍历所有带有 `enumerable` 标志的非 symbol 键，以及原型对象的键。

换句活说，当使用 `Object.getOwnPropertyNames(obj)`、 `Object.getOwnPropertySymbols(obj)`、`Object.keys/values()`、`for..in` 等方法来遍历对象的属性时，会被 ownKeys 捕捉器拦截。

例子，跳过 User 对象中以 \_ 开头的属性：

```JS
let user = {
  name: "John",
  age: 30,
  _password: "***"
};

user = new Proxy(user, {
  ownKeys(target) {
    return Object.keys(target).filter(key => !key.startsWith('_'));
  }
});

// "ownKeys" 过滤掉了 _password
for(let key in user) alert(key); // name，然后是 age

// 对这些方法的效果相同：
alert( Object.keys(user) ); // name,age
alert( Object.values(user) ); // John,30
```

### 具有 “deleteProperty” 和其他捕捉器的受保护属性

以下划线 `_` 开头的属性和方法是内部的，不应从对象外部访问它们，这是约定俗成的。

我们可以使用代理实现阻止对以 `_` 开头属性的任何访问，需要的捕捉器如下：

-  `get` 读取此类属性时抛出错误；
- `set` 写入属性时抛出错误；
- `deleteProperty` 删除属性时抛出错误；
- `ownKeys` 在使用 `for..in` 和像 `Object.keys` 这样的的方法时排除以 `_` 开头的属性。

代码如下：

```JS
let user = {
  name: "John",
  _password: "***"
};

user = new Proxy(user, {
  get(target, prop) {
    if (prop.startsWith('_')) {
      throw new Error("Access denied");
    }
    let value = target[prop];
    return (typeof value === 'function') ? value.bind(target) : value; // (*)
  },
  set(target, prop, val) { // 拦截属性写入
    if (prop.startsWith('_')) {
      throw new Error("Access denied");
    } else {
      target[prop] = val;
      return true;
    }
  },
  deleteProperty(target, prop) { // 拦截属性删除
    if (prop.startsWith('_')) {
      throw new Error("Access denied");
    } else {
      delete target[prop];
      return true;
    }
  },
  ownKeys(target) { // 拦截读取属性列表
    return Object.keys(target).filter(key => !key.startsWith('_'));
  }
});

// "get" 不允许读取 _password
try {
  alert(user._password); // Error: Access denied
} catch(e) { alert(e.message); }

// "set" 不允许写入 _password
try {
  user._password = "test"; // Error: Access denied
} catch(e) { alert(e.message); }

// "deleteProperty" 不允许删除 _password
try {
  delete user._password; // Error: Access denied
} catch(e) { alert(e.message); }

// "ownKeys" 将 _password 过滤出去
for(let key in user) alert(key); // name
```

上面的代码中有些细节需要注意：

```JS
get(target, prop) {
  // ...
  let value = target[prop];
  return (typeof value === 'function') ? value.bind(target) : value; // (*)
}
```

为什么我们需要一个函数去调用 `value.bind(target)`？

原因是对象方法（例如 `user.checkPassword()`）必须能够访问 `_password`：

```JS
user = {
  // ...
  checkPassword(value) {
    //对象方法必须能读取 _password
    return value === this._password;
  }
}
```

对 `user.checkPassword()` 的调用会将被代理的对象 `user` 作为 `this`（点符号之前的对象会成为 `this`），因此，当它尝试访问 `this._password` 时，`get` 捕捉器将激活（在任何属性读取时，它都会被触发）并抛出错误。

因此，我们在 `(*)` 行中将对象方法的上下文绑定到原始对象 `target`。然后，它们将来的调用将使用 `target` 作为 `this`，不会触发任何捕捉器。

该解决方案通常可行，但并不理想，因为一个方法可能会将未被代理的对象传递到其他地方，然后我们就会陷入困境：原始对象在哪里，被代理的对象在哪里？

此外，一个对象可能会被代理多次（多个代理可能会对该对象添加不同的“调整”），并且如果我们将未包装的对象传递给方法，则可能会产生意想不到的后果。

因此，在任何地方都不应使用这种代理。 #question

### 带有 “has” 捕捉器的 “in range”

`has` 捕捉器会拦截 `in` 调用，语法为 has(target, property)，其中：

- target：目标对象；
- property：属性名称。

例子，检查一个数字是否在某个范围内：

```JS
let range = {
  start: 1,
  end: 10
};

range = new Proxy(range, {
  has(target, prop) {
    return prop >= target.start && prop <= target.end;
  }
});

alert(5 in range); // true
alert(50 in range); // false
```

### 包装函数："apply"

我们也可以将代理（proxy）包装在函数周围。

`apply(target, thisArg, args)` 捕捉器能使代理以函数的方式被调用：

- `target` 是目标对象（在 JavaScript 中，函数就是一个对象），
- `thisArg` 是 `this` 的值。
- `args` 是参数列表。
- 
例子：

```JS
function delay(f, ms) {
  return new Proxy(f, {
    apply(target, thisArg, args) {
      setTimeout(() => target.apply(thisArg, args), ms);
    }
  });
}

function sayHi(user) {
  alert(`Hello, ${user}!`);
}

sayHi = delay(sayHi, 3000);

alert(sayHi.length); // 1 (*) proxy 将“获取 length”的操作转发给目标对象

sayHi("John"); // Hello, John!（3 秒后）
```

## 什么是 Reflect

> `Reflect` 是一个内建对象，可简化 `Proxy` 的创建。
>`Reflect` 对象使调用内部方法，例如 `GET`、`SET`，成为了可能。它的方法是内部方法的最小包装。

以下是执行相同操作和 `Reflect` 调用的示例：


| 操作              | Reflect 调用                      | 内部方法  |
| ----------------- | --------------------------------- | --------- |
| obj[prop]         | Reflect.get(obj, prop)            | Get       |
| obj[prop] = value | Reflect.set(obj, prop, value)     | Set       |
| delete obj[prop]  | Reflect.deleteProperty(obj, prop) | Delete    |
| new F(value)      | Reflect.construct(F, value)       | Construct | 
| ...               | ...                               | ...       |

例子：

```JS
let user = {};

Reflect.set(user, 'name', 'John');

alert(user.name); // John
```

从上面的例子中我们看出，`Reflect` 允许我们将操作符（`new`，`delete`，……）作为函数（`Reflect.construct`，`Reflect.deleteProperty`，……）执行调用。

**对于每个可被 `Proxy` 捕获的内部方法，在 `Reflect` 中都有一个对应的方法，其名称和参数与 `Proxy` 捕捉器相同。**

所以，我们可以使用 `Reflect` 来将操作转发给原始对象。

```JS
let user = {
  name: "John",
};

user = new Proxy(user, {
  get(target, prop, receiver) {
    alert(`GET ${prop}`);
    return Reflect.get(target, prop, receiver); // (1)
  },
  set(target, prop, val, receiver) {
    alert(`SET ${prop}=${val}`);
    return Reflect.set(target, prop, val, receiver); // (2)
  }
});

let name = user.name; // 显示 "GET name"
user.name = "Pete"; // 显示 "SET name=Pete"
```

这里：

- `Reflect.get` 读取一个对象属性。
- `Reflect.set` 写入一个对象属性，

这样，一切都很简单：如果一个捕捉器想要将调用转发给对象，则只需使用相同的参数调用 `Reflect.<method>` 就足够了。

在大多数情况下，我们可以在不使用 `Reflect`的情况下完成相同的事情，例如，用于读取属性的 `Reflect.get(target, prop, receiver)` 可以被替换为 `target[prop]`。尽管有一些细微的差别。

说实话，我不太理解这个例子中使用 Reflect 的优势在哪？在 Proxy 中使用 Reflect，这不是多此一举吗？

### Reflect 的优势

前文提到，Reflect 调用的命名与捕捉器的命名完全相同，并接受相同的参数。但是 Reflect 比捕捉器更有一些优势，即 Reflect 提供了一个安全的方式，可以轻松地转发操作，并确保我们不会忘记与此相关的任何内容。我们可以通过代理一个 getter 获取继承对象属性的例子，来直观地理解这种优势。

#### 代理一个 getter

我们有一个带有 `_name` 属性和 getter 的对象 `user`以及对 `user` 对象的一个代理：

```JS
let user = {
  _name: "Guest",
  get name() {
    return this._name;
  }
};

let userProxy = new Proxy(user, {
  get(target, prop, receiver) {
    return target[prop];
  }
});

alert(userProxy.name); // Guest
```

其 `get` 捕捉器在这里是“透明的”，它返回原来的属性，不会做任何其他的事。

下面我们将情况变得复杂一点，让对象 admin 继承 user。不过对象 `admin` 从 `user` 继承后，我们观察到了错误的行为：

```JS
let user = {
  _name: "Guest",
  get name() {
    return this._name;
  }
};

let userProxy = new Proxy(user, {
  get(target, prop, receiver) {
    return target[prop]; // (*) target = user
  }
});

let admin = {
  __proto__: userProxy,
  _name: "Admin"
};

// 期望输出：Admin
alert(admin.name); // 输出：Guest (?!?)
```

读取 `admin.name` 应该返回 `"Admin"`，而不是 `"Guest"`！

发生了什么？或许我们在继承方面做错了什么？

但是，如果我们移除代理，那么一切都会按预期进行。

问题实际上出在代理中，在 `(*)` 行。

1. 当我们读取 `admin.name` 时，由于 `admin` 对象自身没有对应的的属性，搜索将转到其原型。
2. 原型是 `userProxy`。
3. 从代理读取 `name` 属性时，`get` 捕捉器会被触发，并从原始对象返回 `target[prop]` 属性，在 `(*)` 行。当调用 `target[prop]` 时，若 `prop` 是一个 getter，它将在 `this=target` 上下文中运行其代码。因此，结果是来自原始对象 `target` 的 `this._name`，即来自 `user`。

为了解决这种情况，我们需要 `get` 捕捉器的第三个参数 `receiver`。它保证将正确的 `this` 传递给 getter。在我们的例子中是 `admin`。

如何把上下文传递给 getter？对于一个常规函数，我们可以使用 `call/apply`，但这是一个 getter，它不能“被调用”，只能被访问。

`Reflect.get` 可以做到。如果我们使用它，一切都会正常运行，代码如下：

```JS
let user = {
  _name: "Guest",
  get name() {
    return this._name;
  }
};

let userProxy = new Proxy(user, {
  get(target, prop, receiver) { // receiver = admin
    return Reflect.get(target, prop, receiver); // (*)
  }
});


let admin = {
  __proto__: userProxy,
  _name: "Admin"
};

alert(admin.name); // Admin
```

现在 `receiver` 保留了对正确 `this` 的引用（即 `admin`），该引用是在 `(*)` 行中被通过 `Reflect.get` 传递给 getter 的。

我们可以把捕捉器重写得更短：

```JS
get(target, prop, receiver) {
  return Reflect.get(...arguments);
}
```

## Proxy 的局限性

### 内建对象：内部插槽（Internal slot）

许多内建对象，例如 `Map`，`Set`，`Date`，`Promise` 等，都使用了所谓的“内部插槽”。

它们类似于属性，但仅限于内部使用，仅用于规范目的。例如，`Map` 将项目（item）存储在 `[[MapData]]` 中。内建方法可以直接访问它们，而不通过 `[[Get]]/[[Set]]` 内部方法。所以 `Proxy` 无法拦截它们。

### 私有字段

类的私有字段也会发生类似的情况，因为私有字段也是通过内部插槽实现的。JavaScript 在访问它们时不使用 `[[Get]]/[[Set]]`。

### Proxy != target

代理和原始对象是不同的对象。这很自然，对吧？

## 可撤销 Proxy

一个 **可撤销** 的代理是可以被禁用的代理。

假设我们有一个资源，并且想随时关闭对该资源的访问。

我们可以做的是将它包装成可一个撤销的代理，没有任何捕捉器。这样的代理会将操作转发给对象，并且我们可以随时将其禁用。

语法为：

```JS
let {proxy, revoke} = Proxy.revocable(target, handler)
```

该调用返回一个带有 `proxy` 和 `revoke` 函数的对象以将其禁用。

这是一个例子：

```JS
let object = {
  data: "Valuable data"
};

let {proxy, revoke} = Proxy.revocable(object, {});

// 将 proxy 传递到其他某处，而不是对象...
alert(proxy.data); // Valuable data

// 稍后，在我们的代码中
revoke();

// proxy 不再工作（revoked）
alert(proxy.data); // Error
```

对 `revoke()` 的调用会从代理中删除对目标对象的所有内部引用，因此它们之间再无连接。

最初，`revoke` 与 `proxy` 是分开的，因此我们可以传递 `proxy`，同时将 `revoke` 留在当前范围内。

我们也可以通过设置 `proxy.revoke = revoke` 来将 `revoke` 绑定到 `proxy`。

另一种选择是创建一个 `WeakMap`，其中 `proxy` 作为键，相应的 `revoke` 作为值，这样可以轻松找到 `proxy` 所对应的 `revoke`：

```JS
let revokes = new WeakMap();

let object = {
  data: "Valuable data"
};

let {proxy, revoke} = Proxy.revocable(object, {});

revokes.set(proxy, revoke);

// ...我们代码中的其他位置...
revoke = revokes.get(proxy);
revoke();

alert(proxy.data); // Error（revoked）
```

此处我们使用 `WeakMap` 而不是 `Map`，因为它不会阻止垃圾回收。如果一个代理对象变得“不可访问”（例如，没有变量再引用它），则 `WeakMap` 允许将其与它的 `revoke` 一起从内存中清除，因为我们不再需要它了。

## 实践

### 尝试读取不存在的属性时，抛出一个异常

通常，尝试读取不存在的属性会返回 `undefined`。

创建一个代理，在尝试读取不存在的属性时，该代理抛出一个错误。

我自己实现的代码：

```JS
let user = {
    name: "John"
};

function wrap(target) {
    return new Proxy(target, {
        /* 你的代码 */
        get(target, prop) {
            if (prop in target) {
                return target[prop];
            } else {
                throw new Error("ReferenceError: Property doesn't exist: " + prop);
            }
        }
    });
}

user = wrap(user);

alert(user.name); // John
alert(user.age); // ReferenceError: Property doesn't exist: "age"
```

参考代码：

```JS
let user = {
  name: "John"
};

function wrap(target) {
  return new Proxy(target, {
    get(target, prop, receiver) {
      if (prop in target) {
        return Reflect.get(target, prop, receiver);
      } else {
        throw new ReferenceError(`Property doesn't exist: "${prop}"`)
      }
    }
  });
}

user = wrap(user);

alert(user.name); // John
alert(user.age); // ReferenceError: Property doesn't exist: "age"
```

### 访问 array[-1]

自己实现的代码：

```JS
let array = [1, 2, 3];

array = new Proxy(array, {
    get(target, prop) {
        return target[target.length + parseInt(prop)];
    }
});

alert(array[-1]); // 3
alert(array[-2]); // 2

// 其他数组功能应保持“原样”
```

还是存在问题，题目中提到了其他数组功能应该保持“原样”，那我直接访问 array[1] 就会报错，正确的代码如下：

```JS
let array = [1, 2, 3];

array = new Proxy(array, {
  get(target, prop, receiver) {
    if (prop < 0) {
      // 即使我们像 arr[1] 这样访问它
      // prop 是一个字符串，所以我们需要将其转换成数字
      prop = +prop + target.length;
    }
    return Reflect.get(target, prop, receiver);
  }
});


alert(array[-1]); // 3
alert(array[-2]); // 2
```

### 可观察的（Observable）

创建一个函数 `makeObservable(target)`，该函数通过返回一个代理“使得对象可观察”。

其工作方式如下：

```JS
function makeObservable(target) {
  /* 你的代码 */
}

let user = {};
user = makeObservable(user);

user.observe((key, value) => {
  alert(`SET ${key}=${value}`);
});

user.name = "John"; // alerts: SET name=John
```

换句话说，`makeObservable` 返回的对象就像原始对象一样，但是具有 `observe(handler)` 方法，该方法可以将 `handler` 函数设置为在任何属性被更改时，都会被调用的函数。

每当有属性被更改时，都会使用属性的名称和属性值调用 `handler(key, value)` 函数。

P.S. 在本任务中，你可以只关注属性写入。其他的操作可以通过类似的方式实现。

```JS
let handlers = Symbol('handlers');

function makeObservable(target) {
  // 1. 初始化 handler 存储
  target[handlers] = [];

  // 将 handler 函数存储到数组中，以便于之后调用
  target.observe = function(handler) {
    this[handlers].push(handler);
  };

  // 2. 创建一个 proxy 以处理更改
  return new Proxy(target, {
    set(target, property, value, receiver) {
      let success = Reflect.set(...arguments); // 将操作转发给对象
      if (success) { // 如果在设置属性时没有出现 error
        // 调用所有 handler
        target[handlers].forEach(handler => handler(property, value));
      }
      return success;
    }
  });
}

let user = {};

user = makeObservable(user);

user.observe((key, value) => {
  alert(`SET ${key}=${value}`);
});

user.name = "John";
```
## 参考

[Proxy 和 Reflect (javascript.info)](https://zh.javascript.info/proxy#shi-yong-set-bu-zhuo-qi-jin-hang-yan-zheng)