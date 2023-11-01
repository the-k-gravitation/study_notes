### 冒泡排序

```js
/**
 * 冒泡排序
 * @param {*} a
 */
function bubble(a) {
  let count = a.length - 1 // 用来表示总共要大轮几回
  while (true) {
    //用来记录一轮之后，最后进行交易的第一个数值在Array中的索引
    let last = 0
    for (let i = 0; i < count; i++) {
      if (a[i] > a[i + 1]) {
        swap(a, i, i + 1)
        last = i
      }
    }
    count = last
    if (count === 0) {
      // 当count == 0时，就不需要再进行大的轮了
      break
    }
  }
}

function swap(a, i, j) {
  const temp = a[i]
  a[i] = a[j]
  a[j] = temp
}

bubble([5, 2, 7, 4, 1, 3, 8, 9])
```

### 选择排序

每次从反序集中选择其中的最大值或者最小值

属于不稳定的排序算法

```js
function selection(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    // i 代表每轮选择最小元素要交换到目标索引
    let s = i // s 代表每轮选择最小元素的索引
    for (let j = s + 1; j < arr.length; j++) {
      if (arr[j] < arr[s]) {
        s = j
      }
    }
    if (s !== i) {
      swap(arr, s, i)
    }
    console.log(arr)
  }
}

function swap(a, i, j) {
  const temp = a[i]
  a[i] = a[j]
  a[j] = temp
}

selection([5, 3, 7, 2, 1, 9, 8, 4])
```

### 插入排序

### 希尔排序

### 快速排序



