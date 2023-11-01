#Array #Object #数据结构

`Array` 是有序集合。 数组元素是从 `0` 开始编号。

## 创建一个空数组：

```js {.line-numbers}
let arr = new Array();

let arr = []; // 这种方式用得比较多
```

获取数组中的元素：

```js {.line-numbers}
const months = [
  'January',
  'February',
  'March',
  'April',
  'May',
  'June',
  'July',
  'August',
  'September',
  'October',
  'November',
  'December',
];

const mar = months[2]; // March  ,[]中不能使用负数, 会返回 undefined
const dec = months[-1]; // 会返回 undefined
const oct = months.at(-3); // October, 最近才添加到 javascript中的特性，一些老的浏览器需要 使用polyfills
```

## 创建多维数组

```js {.line-numbers}
const twoDArray = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];

console.log(twoDArray[0][0]); // 1
console.log(twoDArray[1][2]); // 6
```

## 数组的 length

数组的 `length` 属性，它表示的是数组最后一个元素的索引值加 1，而不是数组里的元素个数：

```js {.line-numbers}
let arr = [];
arr[100] = 'abc';

console.log(arr.length); // 101
```

`length` 属性是可以被修改的。 如果手动增加 `length`的值，数组原有的元素不会发生变化 , 如果手动减少 `length` 的值，数组会被截断，并且这个过程是不可逆的：

```js {.line-numbers}
let arr = [1, 2, 3];

arr.length = 4;
console.log(arr); // [1,2,3,]

arr.length = 1;
console.log(arr); // [1]
```

清空一个数组，可以直接将它的 `length` 设置为即可： `arr.length = 0`。

## 队列与栈

javascript 中的数组 既可以作 **队列** ， 也可以用作 **栈** 。

对于 `栈` 来说，最后放进去的内容是最先接收的，也叫做 `LIFO`（Last-In-First-Out），即`后进先出`法则。而与`队列`相对应的叫做 `FIFO`（First-In-First-Out），即`先进先出`。

对于 `栈` 的两个操作方法：

- `push()` 在数组末端添加元素：

```js {.line-numbers}
let arr = [1, 2, 3, 4];

arr.push(5);
console.log(arr); // [1,2,3,4,5]

arr.push(6, 7, 8); // 也可以同时添加多个元素
console.log(arr); // [1,2,3,4,5,6,7,8]
```

- `pop()` 取出并返回数组的最后一个元素：

```js {.line-numbers}
let arr = [1, 2, 3];

let n = arr.pop(); // 3
console.log(arr); // [1,2]
```

对于 `队列` 的两个操作方法：

- `unshift()` 在数组的首端添加元素：

```js {.line-numbers}
let arr = [1, 2, 3];

arr.unshift(4);

console.log(arr); // [4, 1, 2, 3]

arr.unshift(5, 6); // 也可以同时添加多个元素
console.log(arr); // [5, 6, 4, 1, 2, 3]
```

- `shift()` 取出数组的第一个元素并返回它：

```js {.line-numbers}
let arr = [1, 2, 3];

let n = arr.shift(); // 1

console.log(arr); // [2,3]
```

`push/pop`  方法运行的比较快，而  `shift/unshift`  比较慢。

`shift`  操作必须做三件事:

1.  移除索引为  `0`  的元素。
2.  把所有的元素向左移动，把索引  `1`  改成  `0`，`2`  改成  `1`  以此类推，对其重新编号。
3.  更新  `length`  属性。
    `unshift()`也会进行类似的操作。
    所以 ，**数组里的元素越多，移动它们就要花越多的时间，也就意味着越多的内存操作**。

`push/pop`  方法不需要移动任何东西。如果从末端移除一个元素，`pop`  方法只需要清理索引值并缩短  `length`  就可以了。

## 遍历数组

```js {.line-numbers}
let arr = [1, 2, 3];

// 第一种遍历方式：
for (let i = 0; i < arr.length; i++) {
  console.log(i);
}

// 第二种遍历方式： for..of
// for..of 不能获取当前元素的索引，只是获取元素值
for (let i of arr) {
  console.log(i);
}
```

`for..in`  循环会遍历  **所有属性**，不仅仅是这些数字属性。对于数组，不应该用  `for..in`  来处理。`for..in`  循环适用于普通对象，并且做了对应的优化。但是不适用于数组，因此速度要慢 10-100 倍。

## toString()

数组的  `toString`  方法会返回以逗号隔开的元素列表的字符串。

```js {.line-numbers}
let arr = [1, 2, 3];

console.log(String(arr)); // "1,2,3"
console.log(arr.toString()); // "1,2,3"
```

数组没有  `Symbol.toPrimitive`，也没有  `valueOf`，它们只能执行  `toString`  进行转换。 当  `"+"`  运算符把一些项加到字符串后面时，加号后面的项也会被转换成字符串。

```js {.line-numbers}
console.log([] + 1); // "1"
console.log([2] + 2); // "22"
console.log([3, 4] + 2); // "3,42"
```

## splice()

`arr.splice()` 方法，可以对数组 **添加，删除和插入元素**。

语法：

```js {.line-numbers}
arr.splice(start [, deleteCount, elem1, ..., elemN]);
```

从索引  `start`  开始修改  `arr`：删除  `deleteCount`  个元素并在当前位置插入  `elem1, ..., elemN`， 最后返回被删除的元素所组成的数组。

```js {.line-numbers}
let arr = [1, 2, 3];

let dels = arr.splice(2, 1); // [3]  , 从索引 2 开始， 删除1个元素
console.log(arr); // [1,2]

arr.splice(0, 0, 4, 5, 6); // 在数组最前面添加3个元素
console.log(arr); // [4,5,6,1,2]

arr.splice(-1, 0, 7, 8); // 在数组末端前一位插入7，8
console.log(arr); // [4, 5, 6, 1, 7, 8, 2]
```

## 遍历：forEach()

语法：

```js {.line-numbers}
arr.forEach(function (item, index, array) {
  // 代码块
});
```

```js {.line-numbers}
[1, 2, 3].forEach((item) => console.log(item * 2)); // 2,4,6

[1, 2, 3].forEach((item, index, array) => {
  console.log(item * 2);
});
```

## filter()

`arr.filter()` 可以对 arr 中的每个元素进行条件过滤，然后将符合条件的元素都返回成一个新的数组。

语法：

```js {.line-numbers}
let results = arr.filter(function (item, index, array) {
  // 过滤逻辑
});
```

```js {.line-numbers}
let arr = [10, 11, 320, 20, 50, 80];

let result = arr.filter((item) => item > 50);
console.log(result); // [320, 80]
```

## map()

`arr.map()` 对数组的每个元素都调用函数，并返回结果数组。

语法：

```js {.line-numbers}
let result = arr.map(function (item, index, array) {
  // 代码块
});
```

```js {.line-numbers}
let arr = [1, 2, 3];

let result = arr.map((item) => item * 3);
console.log(result); // [3,6,9]
```

```js {.line-numbers}
let john = { name: 'John', surname: 'Smith', id: 1 };
let pete = { name: 'Pete', surname: 'Hunt', id: 2 };
let mary = { name: 'Mary', surname: 'Key', id: 3 };

let users = [john, pete, mary];

//JavaScript 在这里会把 `{` 视为函数体的开始，而不是对象的开始。解决方法是将它们包装在普通括号 `()` 中
let usersMapped = users.map((user) => ({
  fullName: `${user.name} ${user.surname}`,
  id: user.id,
}));
```

## reduce()

语法：

```js {.line-numbers}
let result = arr.reduce(function (accumulator, item, index, array) {
  // 代码块
}, initial);
```

- `accumulator` —— 是上一个函数调用的结果，第一次等于  `initial`（如果提供了  `initial`  的话）。
- `item` —— 当前的数组元素。
- `index` —— 当前索引。
- `arr` —— 数组本身。

```js {.line-numbers}
let arr = [1, 2, 3];

let result = arr.reduce((sum, item) => sum + item, 0);
console.log(result);
```

## Iterable object（可迭代对象）

可以应用  `for..of`  的对象被称为  **可迭代的**。

可迭代对象必须实现  `Symbol.iterator`  方法。

- `obj[Symbol.iterator]()`  的结果被称为  **迭代器（iterator）**。由它处理进一步的迭代过程。
- 一个迭代器必须有  `next()`  方法，它返回一个  `{done: Boolean, value: any}`  对象，这里  `done:true`  表明迭代结束，否则  `value`  就是下一个值。
- `Symbol.iterator`  方法会被  `for..of`  自动调用，但我们也可以直接调用它。
- 内建的可迭代对象例如字符串和数组，都实现了  `Symbol.iterator`。
- 字符串迭代器能够识别代理对（surrogate pair）。

```js {.line-numbers}
let range = {
  from: 1,
  to: 10,
};

range[Symbol.iterator] = function () {
  return {
    current: this.from,
    last: this.to,

    next() {
      if (this.current <= this.last) {
        return {
          done: false,
          value: this.current++,
        };
      } else {
        return {
          done: true,
        };
      }
    },
  };
};
```
