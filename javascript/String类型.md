#datatype #string

在 javascript 中， 字符串是不可更改的。
有 3 种表示字符串的方式：

- 双引号： "Hello,World"。
- 单引号： 'Hello,World'。
- 反引号： \`Hello,World\`。

双引号和单引号没有什么区别。 `反引号`是 **功能扩展** 引号，通过它可以将变量或者表达式包装在`${...}`中，嵌入到字符串，方便字符串的操作。

```js {.line-numbers}
let firstName = 'Tom';
let lastName = 'Wu';
let fullName = `${firstName} ${lastName}`; // fullName = ："Tom Wu"

console.log(`1 + 2 = ${1 + 2}`); //输出：1 + 2 = 3
```

可以使用 `for .. of` 遍历字符：

```js {.line-numbers}
for (let char of 'Javascript'){
	console.log(char);
}
```

在 javascript 中没有 character 类型，一个字符串可以包含零个（为空）、一个或者多个字符。

## 字符串转换

可以调用`String(value)`来将`value`转换为字符串类型

```js {.line-numbers}
let v = true;
let vStr = String(v); // "true"

v = null;
vStr = String(v); // "null"
```

 ## 常用函数

### 改变大小写

`toLowerCase()` 和 `toUpperCase()` 方法可以改变大小写：

```js {.line-numbers}
let str = 'Hello, World';
console.log(str.toLowerCase()); // hello, world
console.log(str.toUpperCase()); // HELLO, WORLD
```

### 查找子字符串

- `str.indexOf(substr [, pos])`
在 `str` 中 查找 `substr` ， 如果找到返回匹配成功的位置，否则返回 `-1` 。 `pos` 可选，没有提供时，默认从 `str` 的第一个位置 `0` 开始。

```js {.line-numbers}
let str = 'Hello, World.';

console.log(str.indexOf('o')); // 4
console.log(str.indexOf('o', 5)); // 8

console.log(str.indexOf('ol')); // -1
```

- `str.includes(substr [, pos])`
`str.includes(substr [, pos])` 用来判断 `str` 中是否包含 `substr`，包含返回 `true` ， 否则返回 `false`。

```js {.line-numbers}
let s = 'Hello, World.';

console.log(s.includes(',')); // true
console.log(s.includes('wo', 2)); // false
```

- `str.startsWith(substr)` 和 `str.endsWith(substr)`
`str.startsWith(substr)` 和 `str.endsWith(substr)` 使用比较简单：

```js {.line-numbers}
let s = 'Hello, World.';
console.log(s.startsWith('He')); // true
console.log(s.endsWith('ld')); // false
```

### 获取子字符串

JavaScript 中有三种获取字符串的方法：`substring`、`substr` 和 `slice`。

- `str.slice(start [, end]`
返回字符串 `[start, end)`  的部分。如果 `end` 未提供，返回 `start`到字符串末尾。

```js {.line-numbers}
let s = 'string.slice.function';

console.log(s.slice(0, 6));  // string
console.log(s.slice(0, 1));  // s
console.log(s.slice(10));    // ce.function
```

`start` / `end` 也有可以是负值。 表示从字符串的结尾计算：

```js {.line-numbers}
let s = 'string.slice.function';

console.log(s.slice(-5));  // ction
console.log(s.slice(-5, -1));  // ctio
```

- `str.substring(start [, end])`
用法几乎跟 `str.slice()` 相同，但 它允许 `start` 大于 `end`。

```js {.line-numbers}
let s = 'string.slice.function';

// 两个结果一样
console.log(s.substring(1, 3));  // tr
console.log(s.substring(3, 1));  // tr 

console.log(s.slice(1, 3)); // tr
console.log(s.slice(3, 1));  // "", 不允许 start>end ， 返回空字符串 


// substring(), 不支持负数，它们会被视为 0
console.log(s.substring(-5)); // string.slice.function  , 相当于s.substring(0)

console.log(s.substring(-5, -1)); // ""   , 相当于 s.substring(0, 0)

```

- `str.substr(start [, length]`
返回从 `start` 开始的给定 `length` 长度的字符串部分。 `start` 允许为负数，表示从结尾算起：
```js {.line-numbers}
let s = 'string.slice.function';

console.log(s.substr(0, 6));  // string
console.log(s.substr(-8, 8)); // function
```

|方法|选择方式|负值参数|
|--|--|--|
	|`slice(start, end)`| [start, end) | 允许|
| `substring(start, end)` | \[start, end) | 负值都被视为0 |

