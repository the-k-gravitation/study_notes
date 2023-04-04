#javascript
函数是程序的主要“构建模块”，函数可以使一段代码重复执行，避免代码重复。

## 函数声明

函数以 function 关键字开头，然后是函数的名称，然后是括号之间的“参数”，各个“参数”之间使用逗号分隔。

```js {.line-numbers}
function funcName(parameter1, parameter2,..., parameterN) {
  // 函数体
}
```

## 局部变量

在函数中声明的变量只在该函数体内为可见，也称为局部变量。

```js {.line-numbers}
function showMsg() {
  let msg = 'Hello, World.'; // 局部变量
  console.log(msg);
}

showMsg(); // 执行函数， 输出： Hello, World.

console.log(msg); // 错误！ msg 是 showMsg中的局部变量，外部不能访问
```

## 外部变量（全局变量）

函数对外部变量拥有全部的访问权限。可以对外部变量进行修改。

```js {.line-numbers}
let msg = 'Hello, World.';
function showMsg() {
  msg = 'Hello, javascript';
  console.log(msg);
}

// 函数执行之前
console.log(msg); // Hello, World.
// 执行函数
showMsg(); // Hello, javascript
// 外部变量msg的值被函数修改
console.log(msg); // Hello, javascript
```

函数只有在没有与外部变量同名的局部变量时，才会使用外部变量。如果存在同名的局部变量，则会忽略掉外部变量。

```js {.line-numbers}
let msg = 'Hello, World.';

function showMsg() {
  let msg = 'Hello, javascript';
  console.log(msg);
}

// 函数执行之前
console.log(msg); // Hello, World.
// 执行函数
showMsg(); // Hello, javascript
// 外部变量未被修改
console.log(msg); // Hello, World.
```

## 参数

可以通过参数的形式，将任意数据传递给函数。

```js {.line-numbers}
let firstName = 'John';
let lastName = 'Li';

function getFullName(firstName, lastName) {
  // 此处的firstName,lastName为函数参数中的变量，它们的值为通过执行函数传入的变量的一个局部副本，
  // 它们在函数内部的改变，不会影响到外部变量的值
  // 对于引用类型的数据，有时会改变外部变量的值
  let fullName = `${firstName} ${lastName}`;
  return fullName;
}

let fullName = getFullName(firstName, lastName);
```

两个参数要搞清楚：

- 参数（**parameter**），是函数声明中括号内列出的变量，它是函数声明时的术语
- 参数（**argument**），是函数调用时传递给函数的值，它是函数调用时的术语。

## 默认值

在调用函数时，如果有参数 argument 未被提供，那么相应的值就会变成 `undefined` 。
可以通过在函数声明时，使用 `=` 为参数指定一个“默认”值。

```js {.line-numbers}
// 如果未传递msg的值，则会使用默认的“Javascript”
function showMsg(msg = 'Javascript') {
  console.log(`Hi, ${msg} !`);
}

showMsg('Python'); // Hi, Python !
showMsg(); // Hi, Javascript !
```

默认值可以是更为复杂的表达式，并且只有在当缺少参数时，表达式才会被计算和使用。

```js {.line-numbers}
function showMsg(msg = anotherFun()) {
  //函数体
}
// 此处的anotherFun()只有在执行 showMsg()函数时，msg参数缺少的情况下被执行
```

检查参数是否传递了值:

```js {.line-numbers}
function showMsg(msg) {
  if (msg === undefined) {
    // msg 未传递
  }
  // ...
}

function showMsg(msg) {
  msg = msg || 'no msg given';
  // ...
}
// 使用||时，下面函数调用需要注意！！！！！！
showMsg(0); // no msg given
showMsg(null); // no msg given
showMsg(NaN); // no msg given

function showMsg(msg) {
  // 使用 ?? 更能表示参数是否传递了
  msg = msg ?? 'no msg given';
  // ...
}
```

## 返回值

函数可以将一个值返回到调用它的代码处。

```js {.line-numbers}
function sum(a, b) {
  return a + b;
}

let result = sum('1', '2'); // 12
console.log(result);

result = sum(1, 2); // 3
console.log(result);
```

如果函数体中没有 return 或者 return 后未跟任何返回值，此时函数的返回值为 **undefined** 。

```js {.line-numbers}
function doSomething() {
  // 函数体中没有 return
}

console.log(doSomething() === undefined); // true

function doSomething2() {
  // 函数体中的 return 后没有带任何值
  return;
}
console.log(doSomething2() === undefined); // true
```

## 函数的命名

函数其实就是执行一些行为。所以一种普遍的做法就是用`动词前缀`来开始一个函数，如：

- "get…" —— 返回一个值 , getFullName(...)
- "calc…" —— 计算某些内容 , calcSum(...)
- "create…" —— 创建某些内容, createForm(...)
- "check…" —— 检查某些内容并返回 boolean 值, checkPermission(...)

## 函数表达式

另一种创建函数的语法称为 **函数表达式**

```js {.line-numbers}
//注意： function 关键字后面没有函数名
let showMsg = function () {
  console.log('Hello, javascript');
};

showMsg();
```

在 javascript 中，函数是一个**值**

```js {.line-numbers}
// 创建
function showMsg() {
  console.log('Say, Hello.');
}

let func = showMsg; // 将showMsg赋值给 func变量

func();
showMsg();
```

- 函数表达式是在代码执行到达时才被创建，并且仅从那一刻起才可用。
- 严格模式下，当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。

## 回调函数

可以将函数作为值来传递

```js {.line-numbers}
function isPermission(isPermission, yes, no) {
  if (isPermission) {
    yes();
  } else {
    no();
  }
}

isPermission(
  true,
  // 匿名函数
  function () {
    console.log('我已经有权限了');
  },
  function () {
    console.log('对不起，我的权限暂时不够');
  }
);
```

## 箭头函数 =>

```js {.line-numbers}
// 创建了一个箭头函数 func，它接受参数 arg1..argN个参数，然后使用参数对右侧的 expression 求值并返回其结果。
let func = (arg1, arg2, ..., argN) => expression;

// 与上面等同
let func = function (arg1, arg2, ..., argN){
  return expression;
}
```

- 如果只有一个参数，可以省略掉参数外的圆括号

```js {.line-numbers}
let getDouble = (n) => n * 2;

getDouble(10); // 20
```

- 如果没有参数，圆括号必须保留

```js {.line-numbers}
let showMsg = () => console.log('Hello,javascript');

showMsg();
```

- 如果箭头函数的函数体，不止一行语句时，需要把函数体放在花括号中

```js {.line-numbers}
let sum = (a, b) => {
  let result = a + b;
  return result;
};

sum(10, 20); // 30
```


## 闭包

[闭包](https://en.wikipedia.org/wiki/Closure_(computer_programming)) 是指一个函数可以记住其外部变量并可以访问这些变量。

## setTimeout & setInterval

- `setTimeout(func, delay, ...args)` 和 `setInterval(func, delay, ...args)` 方法允许我们在 `delay` 毫秒之后运行 `func` 一次或以 `delay` 毫秒为时间间隔周期性运行 `func`。

```js {.line-numbers}
function sayHi(phrase, who) { alert( phrase + ', ' + who ); } setTimeout(sayHi, 1000, "Hello", "John");
```

- 要取消函数的执行，我们应该调用 `clearInterval/clearTimeout`，并将 `setInterval/setTimeout` 返回的值作为入参传入。

```js {.line-numbers}
let timerId = setTimeout(...); 
clearTimeout(timerId);


// 每 2 秒重复一次 
let timerId = setInterval(() => alert('tick'), 2000); 
// 5 秒之后停止 
setTimeout(() => { clearInterval(timerId); alert('stop'); }, 5000);
```

- 嵌套的 `setTimeout` 比 `setInterval` 用起来更加灵活，允许我们更精确地设置两次执行之间的时间。

```js {.line-numbers}
let timerId = setTimeout(function tick() { 
	alert('tick'); 
	timerId = setTimeout(tick, 2000); 
}, 2000);
```

- 零延时调度 `setTimeout(func, 0)`（与 `setTimeout(func)` 相同）用来调度需要尽快执行的调用，但是会在当前脚本执行完成后进行调用。
- 浏览器会将 `setTimeout` 或 `setInterval` 的五层或更多层嵌套调用（调用五次之后）的最小延时限制在 4ms。这是历史遗留问题。


## 装饰器

**装饰器** 是一个围绕改变函数行为的包装器。主要工作仍由该函数来完成。

- [func.call(context, arg1, arg2…)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Function/call) —— 用给定的上下文和参数调用 `func`。
- [func.apply(context, args)](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Function/apply) —— 调用 `func` 将 `context` 作为 `this` 和类数组的 `args` 传递给参数列表。

```js {.line-numbers}
function spy(func) {
	function wrapper(...args) {
		// using ...args instead of arguments to store "real" array in wrapper.calls
		wrapper.calls.push(args);
		return func.apply(this, args);
	}

	wrapper.calls = [];
	return wrapper;
}

function work(a, b) {
	console.log(a + b); // work 是一个任意的函数或方法
}


work = spy(work);

work(1, 2); // 3
work(4, 5); // 9

  
for (let args of work.calls) {
	console.log(args);
	console.log('call:' + args.join()); // "call:1,2", "call:4,5"
}
```