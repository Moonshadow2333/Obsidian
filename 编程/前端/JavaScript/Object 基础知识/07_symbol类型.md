## 前言

在 JavaScript 中，只有两种原始类型可以作为对象属性键：

- 字符串类型；
- symbol 类型。
 
如果使用其他类型，例如数字，都会自动转换成字符串。即 object[1] 和 object["1"] 相同，object[true] 和 object["true"] 相同。

这篇笔记用来探讨 symbol 类型的特点。

## 什么是 symbol？

> “symbol” 值表示唯一的标识符。

创建 symbol：

```JS
let id = Symbol();
```

创建时，我们可以给 symbol 一个描述（也称为 symbol 名）：

```JS
// id 是描述为 "id" 的 symbol
let id = Symbol("id");
```

symbol 值是唯一的。**即使我们创建了许多具有相同描述的 symbol，它们的值也是不同**。描述只是一个标签，不影响任何东西。

例如，这里有两个描述相同的 symbol —— 它们不相等：

```JS
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

总之，symbol 是带有可选描述的“原始唯一值”。

## symbol 不会被自动转换为字符串

在 Java 中大多数值都支持字符串的隐式转换。例如，我们可以 `alert` 任何值，都可以生效。symbol 比较特殊，它不会被自动转换。

例如，这个 `alert` 将会提示出错：

```JS
let id = Symbol("id");
alert(id); // 类型错误：无法将 symbol 值转换为字符串。
```

symbol 虽然不会隐式转换成字符串，但是可以被显示地转换成字符串，转换的方法就是在它上面调用 `.toString()`，如下所示：

```JS
let id = Symbol("id");
alert(id.toString()); // Symbol(id)，现在它有效了
```

或者获取 symbol.description 属性，只显示描述：

```JS
let id = Symbol("id");
alert(id.description); // id
```

## “隐藏”属性

这段内容先抄下来，目前还不直到该怎么用。

symbol 允许我们创建对象的“隐藏”属性，代码的任何其他部分都不能意外访问或重写这些属性。

例如，如果我们使用的是属于第三方代码的 `user` 对象，我们想要给它们添加一些标识符。

我们可以给它们使用 symbol 键：

```JS
let user = { // 属于另一个代码
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // 我们可以使用 symbol 作为键来访问数据
```

使用 `Symbol("id")` 作为键，比起用字符串 `"id"` 来有什么好处呢？

由于 `user` 对象属于另一个代码库，所以向它们添加字段是不安全的，因为我们可能会影响代码库中的其他预定义行为。但 symbol 属性不会被意外访问到。第三方代码不会知道新定义的 symbol，因此将 symbol 添加到 `user` 对象是安全的。

另外，假设另一个脚本希望在 `user` 中有自己的标识符，以实现自己的目的。

那么，该脚本可以创建自己的 `Symbol("id")`，像这样：

```JS
// ...
let id = Symbol("id");

user[id] = "Their id value";
```

我们的标识符和它们的标识符之间不会有冲突，因为 symbol 总是不同的，即使它们有相同的名字。

……但如果我们处于同样的目的，使用字符串 `"id"` 而不是用 symbol，那么 **就会** 出现冲突：

```JS
let user = { name: "John" };

// 我们的脚本使用了 "id" 属性。
user.id = "Our id value";

// ……另一个脚本也想将 "id" 用于它的目的……

user.id = "Their id value"
// 砰！无意中被另一个脚本重写了 id！
```

## 对象字面量中的 symbol

如果我们要在对象字面量 `{...}` 中使用 symbol，则需要使用方括号把它括起来。例如：

```JS
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // 而不是 "id"：123
};
```

## symbol 在 for...in 中会被跳过

symbol 属性不参与 `for..in` 循环。例如：

```JS
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

for (let key in user) alert(key); // name, age（没有 symbol）

// 使用 symbol 任务直接访问
alert("Direct: " + user[id]); // Direct: 123
```

[Object.keys(user)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) 也会忽略它们。这是一般“隐藏符号属性”原则的一部分。如果另一个脚本或库遍历我们的对象，它不会意外地访问到符号属性。

相反，[Object.assign](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) 会同时复制字符串和 symbol 属性：

```JS
let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123
```

这里并不矛盾，就是这样设计的。这里的想法是当我们克隆或者合并一个 object 时，通常希望 **所有** 属性被复制（包括像 `id` 这样的 symbol）。

## 全局 symbol

正如我们所看到的，通常所有的 symbol 都是不同的，即使它们有相同的名字。但有时我们想要名字相同的 symbol 具有相同的实体。

**全局 symbol 注册表**。我们可以在其中创建 symbol 并在稍后访问它们，它可以确保每次访问相同名字的 symbol 时，返回的都是相同的 symbol。

要从注册表中读取（不存在则创建）symbol，请使用 `Symbol.for(key)`。

该调用会检查全局注册表，如果有一个描述为 `key` 的 symbol，则返回该 symbol，否则将创建一个新 symbol（`Symbol(key)`），并通过给定的 `key` 将其存储在注册表中。例如：

```JS
// 从全局注册表中读取
let id = Symbol.for("id"); // 如果该 symbol 不存在，则创建它

// 再次读取（可能是在代码中的另一个位置）
let idAgain = Symbol.for("id");

// 相同的 symbol
alert( id === idAgain ); // true
```

注册表内的 symbol 被称为 **全局 symbol**。如果我们想要一个应用程序范围内的 symbol，可以在代码中随处访问 —— 这就是它们的用途。

## symbol.keyFor

我们已经看到，对于全局 symbol，`Symbol.for(key)` 按名字返回一个 symbol。相反，通过全局 symbol 返回一个名字，我们可以使用 `Symbol.keyFor(sym)`，例如：

```JS
// 通过 name 获取 symbol
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 通过 symbol 获取 name
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

`Symbol.keyFor` 内部使用全局 symbol 注册表来查找 symbol 的键。所以它不适用于非全局 symbol。如果 symbol 不是全局的，它将无法找到它并返回 `undefined`。

但是，所有 symbol 都具有 `description` 属性。例如：

```JS
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name，全局 symbol
alert( Symbol.keyFor(localSymbol) ); // undefined，非全局

alert( localSymbol.description ); // name
```

## 系统 symbol

JavaScript 内部有很多“系统” symbol，我们可以使用它们来微调对象的各个方面。

它们都被列在了 [众所周知的 symbol](https://tc39.github.io/ecma262/#sec-well-known-symbols) 表的规范中：

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ……等等。

例如，`Symbol.toPrimitive` 允许我们将对象描述为原始值转换。我们很快就会看到它的使用。

当我们研究相应的语言特征时，我们对其他的 symbol 也会慢慢熟悉起来。

## 实践

## 参考

[symbol 类型 (javascript.info)](https://zh.javascript.info/symbol)