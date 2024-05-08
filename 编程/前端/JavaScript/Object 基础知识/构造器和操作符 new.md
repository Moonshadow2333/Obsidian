
- 构造函数，或简称构造器，就是常规函数，但大家对于构造器有个共同的约定，就是其命名首字母要大写。
- 构造函数只能使用 `new` 来调用。这样的调用意味着在开始时创建了空的 `this`，并在最后返回填充了值的 `this`。

```JS
function User(name) {
  // this = {};（隐式创建）

  // 添加属性到 this
  this.name = name;
  this.isAdmin = false;

  // return this;（隐式返回）
}
```

## 实践

### 创建 new Calculator

创建一个构造函数 `Calculator`，它创建的对象中有三个方法：

- `read()` 使用 `prompt` 请求两个值并把它们记录在对象的属性中（这个要求和[[对象方法，this#创建一个计算器|之前创建一个计算器任务的要求类似]]）。
- `sum()` 返回这些属性的总和。
- `mul()` 返回这些属性的乘积。

```JS
let calculator = new Calculator();
calculator.read();

alert( "Sum=" + calculator.sum() );
alert( "Mul=" + calculator.mul() );
```
我的答案：

```JS
let calculator = new Calculator();

function Calculator() {
	this.read = function() {
		this.a = +prompt('a', 0);
		this.b = +prompt('b', 0);
	};
	this.sum = function() {
		return this.a + this.b;
	};
	this.mul = function() {
		return this.a * this.b;
	}
}
calculator.read();

alert("Sum=" + calculator.sum());
alert("Mul=" + calculator.mul());
```

参考答案：

```JS
function Calculator() {

  this.read = function() {
    this.a = +prompt('a?', 0);
    this.b = +prompt('b?', 0);
  };

  this.sum = function() {
    return this.a + this.b;
  };

  this.mul = function() {
    return this.a * this.b;
  };
}

let calculator = new Calculator();
calculator.read();

alert( "Sum=" + calculator.sum() );
alert( "Mul=" + calculator.mul() );
```

### 创建 new Accumulator

创建一个构造函数 `Accumulator(startingValue)`。

它创建的对象应该：

- 将“当前 value”存储在属性 `value` 中。起始值被设置到构造器 `startingValue` 的参数。
- `read()` 方法应该使用 `prompt` 来读取一个新的数字，并将其添加到 `value` 中。

换句话说，`value` 属性是所有用户输入值与初始值 `startingValue` 的总和。

下面是示例代码：

```JS
let accumulator = new Accumulator(1); // 初始值 1

accumulator.read(); // 添加用户输入的 value
accumulator.read(); // 添加用户输入的 value

alert(accumulator.value); // 显示这些值的总和
```

我的答案：

```JS
let accumulator = new Accumulator(1); // 初始值 1

accumulator.read(); // 添加用户输入的 value
accumulator.read(); // 添加用户输入的 value

alert(accumulator.value); // 显示这些值的总和

function Accumulator(startingValue) {
	this.value = startingValue;
	this.read = function() {
		this.value += +prompt('a', 0);
		alert(this.value);
	}
}
```

参考答案：

```JS
function Accumulator(startingValue) {
  this.value = startingValue;

  this.read = function() {
    this.value += +prompt('How much to add?', 0);
  };

}

let accumulator = new Accumulator(1);
accumulator.read();
accumulator.read();
alert(accumulator.value);
```

## 参考

[构造器和操作符 "new" (javascript.info)](https://zh.javascript.info/constructor-new#tasks)