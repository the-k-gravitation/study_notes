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

```js {.line-numbers}
let recipeMap = new Map([ ['cucumber', 500], ['tomatoes', 350], ['onion', 50] ]); 

// 遍历所有的键（vegetables） 
for (let vegetable of recipeMap.keys()) { 
	alert(vegetable); // cucumber, tomatoes, onion 
} 

// 遍历所有的值（amounts） 
for (let amount of recipeMap.values()) { 
	alert(amount); // 500, 350, 50 
} 

// 遍历所有的实体 [key, value] 
for (let entry of recipeMap) { 
	// 与 recipeMap.entries() 相同 
	alert(entry); // cucumber,500 (and so on) 
}
```

迭代的顺序与插入值的顺序相同。与普通的 `Object` 不同，`Map` 保留了此顺序。

## Set

`Set` 是一个特殊的类型集合 —— “值的集合”（没有键），它的每一个值只能出现一次。

它的主要方法如下：

- `new Set(iterable)` —— 创建一个 `set`，如果提供了一个 `iterable` 对象（通常是数组），将会从数组里面复制值到 `set` 中。
- `set.add(value)` —— 添加一个值，返回 set 本身
- `set.delete(value)` —— 删除值，如果 `value` 在这个方法调用的时候存在则返回 `true` ，否则返回 `false`。
- `set.has(value)` —— 如果 `value` 在 set 中，返回 `true`，否则返回 `false`。
- `set.clear()` —— 清空 set。
- `set.size` —— 返回元素个数。

```js {.line-numbers}
let set = new Set(); 

let john = { name: "John" };
let pete = { name: "Pete" }; 
let mary = { name: "Mary" }; 

// visits，一些访客来访好几次 
set.add(john); 
set.add(pete); 
set.add(mary); 
set.add(john); 
set.add(mary); 

// set 只保留不重复的值 
alert( set.size ); // 3 

for (let user of set) { 
	alert(user.name); // John（然后 Pete 和 Mary）
}
```

## WeakMap & WeakSet

`WeakMap` 和 `WeakSet` 被用作“主要”对象存储之外的“辅助”数据结构。一旦将对象从主存储器中删除，如果该对象仅被用作 `WeakMap` 或 `WeakSet` 的键，那么该对象将被自动清除。

它们的主要优点是它们对对象是弱引用，所以被它们引用的对象很容易地被垃圾收集器移除。

`WeakMap` 是类似于 `Map` 的集合，它仅允许对象作为键，并且一旦通过其他方式无法访问这些对象，垃圾回收便会将这些对象与其关联值一同删除。

`WeakSet` 是类似于 `Set` 的集合，它仅存储对象，并且一旦通过其他方式无法访问这些对象，垃圾回收便会将这些对象删除。

`WeakMap` 和 `WeakSet` 最明显的局限性就是不能迭代，并且无法获取所有当前内容。

`WeakMap` 和 `Map` 的第一个不同点就是，`WeakMap` 的键必须是对象，不能是原始值：

```js {.line-numbers}
let cache = new WeakMap();

let obj = {};

cache.set(obj, 'obj');

obj = null; 

// obj 被从内存中删除，该对象将会被从内存（和map）中自动清除。
```

```js {.line-numbers}
const cache = new WeakMap();

function process(obj) {
	if (!cache.has(obj)) {
		let result = /*计算一个结果*/ 1;
		cache.set(obj, result);
	}

	return cache.get(obj);
}

const obj = {}; // 一个逻辑对象

const r1 = process(obj);
const r2 = process(obj);

obj = null; 

// 当 obj 被垃圾回收后，缓存中的数据也会被清除
```

```js {.line-numbers}
let visitedSet = new WeakSet(); 

let john = { name: "John" }; 
let pete = { name: "Pete" }; 
let mary = { name: "Mary" }; 

visitedSet.add(john); // John 访问了我们 
visitedSet.add(pete); // 然后是 Pete 
visitedSet.add(john); // John 再次访问 

// visitedSet 现在有两个用户了 
// 检查 John 是否来访过？ 
alert(visitedSet.has(john)); // true 

// 检查 Mary 是否来访过？ 
alert(visitedSet.has(mary)); // false 

john = null; 

// visitedSet 将被自动清理(即自动清除其中已失效的值 john)
```


