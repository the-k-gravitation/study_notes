#Array #Object #数据结构

`Array` 是有序集合。  数组元素是从 `0` 开始编号。

## 创建一个空数组：

```js {.line-numbers}
let arr = new Array();

let arr = []; // 这种方式用得比较多
```

获取数组中的元素：

```js {.line-numbers}
const months = [
  "January",
  "February",
  "March",
  "April",
  "May",
  "June",
  "July",
  "August",
  "September",
  "October",
  "November",
  "December"
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
  [7, 8, 9]
];

console.log(twoDArray[0][0]); // 1
console.log(twoDArray[1][2]); // 6
```

## 数组的 length

数组的 `length` 属性，它表示的是数组最后一个元素的索引值加1，而不是数组里的元素个数：

```js {.line-numbers}
let arr = [];
arr[100] = 'abc';

console.log(arr.length); // 101
```

`length` 属性是可以被修改的。 如果手动增加 `length`的值，数组原有的元素不会发生变化 , 如果手动减少 `length` 的值，数组会被截断，并且这个过程是不可逆的：

```js {.line-numbers}
let arr = [1,2,3];

arr.length = 4;
console.log(arr); // [1,2,3,]   

arr.length = 1;
console.log(arr); // [1]
```

清空一个数组，可以直接将它的 `length` 设置为即可： `arr.length = 0`。

javascript 中的数组 既可以作 **队列** ， 也可以用作 **栈** 。

对于 `栈` 来说，最后放进去的内容是最先接收的，也叫做 `LIFO`（Last-In-First-Out），即`后进先出`法则。而与`队列`相对应的叫做 `FIFO`（First-In-First-Out），即`先进先出`。

对于 `栈` 的两个操作方法：
- `push()` 在数组末端添加元素：
```js {.line-numbers}
let arr = [1,2,3,4];

arr.push(5);
console.log(arr); //
```
- `pop()` 取出并返回数组的最后一个元素：

对于 `队列` 的两个操作方法：


