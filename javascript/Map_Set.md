#Map #Set #数据结构 

## Map

`Map` 是一个带键的数据项的集合，就像一个 `Object` 一样。 但是它们最大的差别是 `Map` 允许任何类型的键（key）。

它的方法和属性如下：

- `new Map()` —— 创建 map。
- `map.set(key, value)` —— 根据键存储值。
- `map.get(key)` —— 根据键来返回值，如果 `map` 中不存在对应的 `key`，则返回 `undefined`。
- `map.has(key)` —— 如果 `key` 存在则返回 `true`，否则返回 `false`。
- `map.delete(key)` —— 删除指定键的值。
- `map.clear()` —— 清空 map。
- `map.size` —— 返回当前元素个数。

```js {.line-numbers}
let map = new Map(); 

map.set('1', 'str1'); // 字符串键 
map.set(1, 'num1'); // 数字键 
map.set(true, 'bool1'); // 布尔值键 
// 还记得普通的 Object 吗? 它会将键转化为字符串 // Map 则会保留键的类型，所以下面这两个结果不同： 
console.log( map.get(1) ); // 'num1' 
console.log( map.get('1') ); // 'str1'
```

## Set

