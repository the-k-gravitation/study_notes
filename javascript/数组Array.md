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

`length` 属性是可以被修改的。 如果手动增加 `length`的值，会在数组的后面添加相应的 `null` , 如果

