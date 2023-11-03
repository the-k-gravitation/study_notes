 #datatype #number

`number`类型代表**整数**和**浮点数**。

```js {.line-numbers}
let num = 100;
num = 1.2345;

let n = 8999999999;

// 下划线 `_` 使得数字具有更强的可读性
let n1 = 8_999_999_999;
console.log(n === n1); // true

let n2 = 1e5; // 科学计数法
let n3 = 100000;
console.log(n2 === n3); // true

let n4 = 1e-5;
let n5 = 1 / 100000;
console.log(n4 === n5); // true
```

除了常规的数字外，还包括几个“**特殊数值**”：`Infinity`、`-Infinity`和`NaN`。

- `Infinity` 表示**无穷大(正无穷) ∞**，`-Infinity`表示**无穷小(负无穷)-∞**。

  ```js {.line-numbers}
  let n = 10 / 0; // 通过除以 0 ，可以得到 Infinity
  let n2 = Infinity; // 可以直接使用Infinity来进行赋值

  let n3 = -10 / 0; // 会得到-Infinity
  ```

- `NaN` 表示**计算错误**。 它是一个不正确或者一个未定义的数学操作所得到的结果。

  ```js {.line-numbers}
  let n3 = 'Tom' / 2;
  console.log(n3); // NaN
  console.log(NaN + 10); // NaN
  console.log(NaN * 10); // NaN
  ```

任何对 **NaN** 的数学运算都会返回 `NaN`，只有一个例外：**NaN \*\* 0 = 1**。

`NaN` 是独一无二的，它不等于任何东西，包括它自身：

```js {.line-numbers}
console.log(NaN === NaN); // false
```

在 `javascript` 中做数学运算是安全的。脚本永远不会因为一个致命的数学运算而停止，最坏的情况，会得到 `NaN` 的结果。

## 十六进制、二进制和八进制

javascript 可以直接坚持 十六进制、二进制和八进制数字的编写：

```js {.line-numbers}
let a = 0xff; // 255

let b = 0b11111111; // 255

let c = 0o377; // 255

console.log(a === b); // true
console.log(b === c); // true
```

对于其他进制，可以使用 `parseInt()` 函数。

## toString(base)

`number.toString(base)` 用于返回 `number` 给定的 `base` 进制数字 的字符串。

```js {.line-numbers}
let num = 123;

console.log(num.toString(16)); // 7b
console.log(num.toString(8)); // 173
console.log(num.toString(2)); // 1111011
```

`base=36` 是最大进制。 可以用来将一个较长的数字标识符转换成较短的：

```js {.line-numbers}
let n = (12345664554).toString(36);
let n = (12345664554).toString(36); // 注意使用两个点
// 当直接将数字使用toString()时，可以使用上面 两种方式。
```

## 舍入

- Math.floor()

`向下`舍入：10.2 --> 10， `-10.2 --> -11` 。

- Math.ceil()

`向上`舍入： 10.2 --> 11， `-10.2 --> -10` 。

- Math.round()

`四舍五入` 向最近的整数舍入： 10.2 --> 10， `-10.5 --> -10`， -10.6 --> -11。

- Math.trunc()

移除小数点后面的所有内容而没有舍入（ _IE 浏览器不支持这个方法_ ） ： 10.2 --> 10， -10.2 --> -10 。

- toFixed(n)

`toFixed(n)` 将数字舍入到小数点后 `n` 位，并以 `字符串` 的形式返回。
`toFixed(n)` 会将数字舍入到最接近的值， 类似于 `Math.round()` 。
如果 `n` 比数字所有的小数位还多，则结尾会添加零。

```js {.line-numbers}
let n1 = 10.27;
console.log(n1.toFiexed(1)); /// "10.3"

let n2 = 10.24;
console.log(n2.toFixed(1)); // "10.2"

let n3 = 10.25;
console.log(n3.toFixed(3)); // "10.250"
```

可以通过 一元加号 或 `Number()` 调用，将其转换为数字 ：

```js {.line-numbers}
let n = 10.237843;

n = +n.toFixed(2);
n = Number(n.toFixed(2));
```

`Math.round` 和 `toFixed` 都将数字舍入到最接近的数字：`0..4` 会被舍去，而 `5..9` 会进一位。

还可以使用 `toFixed()`来检查一个数字的精度损失情况：

```js {.line-numbers}
console.log((6.35).toFixed(20)); // 6.34999999999999964473
// 所以 6.35 保留一位小数位时，会得到 6.3,而不是6.4
console.log((6.35).toFixed(1)); // 6.3


console.log((1.35).toFixed(20)); // 1.35000000000000008882
// 1.35 保留一位小数位时，会得到 1.4
console.log((1.35).toFixed(1)); // 1.4

```

## 不精确的计算

javascript 在内部，数字是以 64 位格式 [IEEE-754](http://en.wikipedia.org/wiki/IEEE_754) 表示的，所以正好有 `64` 位可以存储一个数字：其中 `52` 位被用于存储这些数字，其中 `11` 位用于存储小数点的位置，而 `1` 位用于符号。

处理精度损失最可靠的方式就是使用方法 `toFixed(n)` 对结果进行舍入：

```js {.line-numbers}
let sum = 0.1 + 0.2;  // 0.30000000000000004

// 使用tofixed()对计算之后的结果进行小数点的舍入，再将其转换为数字
sum = +sum.toFixed(2);
```

## isNaN(value) 与 isFinite(value)

`isNaN(value)` 用来测试 `value` 是否为 `NaN`：

```js {.line-numbers}
console.log(isNaN(NaN)); // true
console.log(isNaN(Infinity)); // false
console.log(isNaN('abc')); // true
```

`isFinite(value)`  将其参数转换为数字，如果是常规数字而不是 `NaN/Infinity/-Infinity`，则返回 `true`：

```js {.line-numbers}
console.log(isFinite('10')); // true
console.log(isFinite('')); // true
console.log(isFinite(null)); // true
console.log(isFinite('abc')); // false
console.log(isFinite(Infinity)); // false
console.log(isFinite(NaN)); // false
```

可以 使用 `isFinite(value)` 来验证字符串值是不是一个常规的数字：

```js {.line-numbers}
let n = +prompt('输入一个数字：', '');
n = isFinite(n);
```

<font color="red">所有的数字函数， 都将 空字符串 或仅有 空格的字符串 视为 0</font> 。

## ===  与 Object.is

除了以下两种情况下， `===` 与 `Object.is` 完全一样：

1. `Object.is(NaN , NaN) === true`
2. `Object.is(0, -0) === false`， 在内部，数字的符号位可能会不同，即使其他所有位均为零。

当内部算法需要比较两个值是否完全相同时，它使用 `Object.is`（内部称为 [SameValue](https://tc39.github.io/ecma262/#sec-samevalue)）。

## 数字型转换

可以调用`Number(value)`来将`value`转换为 number 类型。

```js {.line-numbers}
let str = '   100   ';
let n = Number(str); // 100

str = '';
n = Number(str); // 0

str = undefined;
n = Number(str); // NaN

str = null;
n = Number(str); // 0

str = true;
n = Number(str); // 1

str = '100abcd';
n = Number(str); // NaN
```

也可以使用一元加号实现相同的转换。

```js {.line-numbers}
let str = '   100   ';
let n = +str; // 100

console.log(+'10px'); // NaN

```

使用加号  `+` 和 `Number()` 的数字转换是严格的， 唯一的例外是字符串开头或结尾的空格，因为它们会被忽略。

**Number()** 类型转换规则：

| 值            | 转换之后的结果                                                                                                                                                                           |
| :------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| undefined     | NaN                                                                                                                                                                                      |
| null          | 0                                                                                                                                                                                        |
| true 和 false | 1 和 0                                                                                                                                                                                   |
| string        | 去掉首尾空白字符（空格、换行符 \n、制表符 \t 等）后的纯数字字符串中含有的数字。如果剩余字符串为空，则转换结果为 0。否则，将会从剩余字符串中“读取”数字。当类型转换出现 error 时返回 NaN。 |

## parseInt 和 parseFloat

`parseInt()`  与 `parseFloat()` 用来从一个字符串中提取一个有效的数字。
函数 `parseInt` 返回一个整数，而 `parseFloat` 返回一个浮点数：

```js {.line-numbers}
console.log(parseInt('  10x')); // 10
console.log(parseInt('   a10px')); // NaN
console.log(parseInt('   10  22 33 x')); // 10
console.log(parseInt('10.1')); // 10


console.log(parseFloat('  10.5m')); // 10.5
console.log(parseFloat('   10.1.1.23x'));  // 10.1
console.log(parseFloat('   a313.2')); // NaN
```

`parseInt()` 函数还可以 提供第二个参数 ，它用来指定数字的基数：

```js {.line-numbers}
console.log(parseInt('0xfc', 16)); // 252
console.log(parseInt('abcc', 16)); // 43980
console.log(parseInt('10110', 2)); // 22
console.log(parseInt('2n3cr', 36)); // 4436667
```

## 解题

### 从 min 到 max 的随机数

内建函数 `Math.random()` 会创建一个在 `0` 到 `1` 之间（不包括 `1`）的随机数。

编写一个 `random(min, max)` 函数，用以生成一个在 `min` 到 `max` 之间的随机浮点数（不包括 `max`)）。

需要将区间 0…1 中的所有值“映射”为范围在 `min` 到 `max` 中的值。
分两个阶段完成：

1. 如果我们将 0…1 的随机数乘以 `max-min`，则随机数的范围将从 0…1 增加到 `0..max-min`。
2. 现在，如果我们将随机数与 `min` 相加，则随机数的范围将为 `min` 到 `max`。
3.

```js {.line-numbers}
function random(min, max) { 
 return min + Math.random() * (max - min); 
}
```

### 从 min 到 max 的随机整数

# 解题

创建一个函数 `randomInteger(min, max)`，该函数会生成一个范围在 `min` 到 `max` 中的随机整数，包括 `min` 和 `max`。
在 `min..max` 范围中的所有数字的出现概率必须相同。

#### 错误的解决方案

最简单但错误的解决方案是生成一个范围在 `min` 到 `max` 的值，并取对其进行四舍五入后的值：

```js {.line-numbers}
// 但不正确。获得边缘值 `min` 和 `max` 的概率比其他值低两倍。
function randomInteger(min, max) {
 let rand = min + Math.random() * (max - min); 
 return Math.round(rand); 
}

randomInteger(1, 3);
// 发生这种情况是因为 `Math.round()` 从范围 `1..3` 中获得随机数，并按如下所示进行四舍五入：
/*
values from 1 ... 1.4999999999 ---> 1    （0.5）
values from 1.5 ... 2.4999999999 ---> 2    （1）
values from 2.5 ... 2.9999999999 ---> 3   (0.5)
*/
```

#### 正确的解决方案

有很多正确的解决方案。其中之一是调整取值范围的边界。为了确保相同的取值范围，我们可以生成从 0.5 到 3.5 的值，从而将所需的概率添加到取值范围的边界：

```js {.line-numbers}
function randomInteger(min, max) { 
 // 现在范围是从 (min-0.5) 到 (max+0.5) 
 let rand = min - 0.5 + Math.random() * (max - min + 1); 
 return Math.round(rand); 
}
```

另一种方法是使用 `Math.floor` 来取范围从 `min` 到 `max+1` 的随机数：

```js {.line-numbers}
function randomInteger(min, max) { 
 // here rand is from min to (max+1) 
 let rand = min + Math.random() * (max + 1 - min); 
 return Math.floor(rand); 
}
```
