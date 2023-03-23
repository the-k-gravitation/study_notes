#datatype #symbol

## 创建Symbol类型

`Symbol` 是唯一标识符的基本类型。 
使用 `Symbol()` 或 `Symbol(descriptoin)` 来创建：

```js {.line-numbers}
let id = Symbol();

// "id" 是 id2 的描述 或者 symbol名
let id2 = Symbol('id');
```

`Symbol` 保证是唯一的，即使创建了许多具有相同描述的 Symbol， 它们的值也是不同的。描述只是一个标签，不影响任何值。
`Symbol` 不会被自动转换为字符串。 可以通过 `Symbol.description` 获取 描述。
```js {.line-numbers}
let id1 = Symbol('id');
let id2 = Symbol('id');

console.log(id1 == id2); // false

console.log(id1.toString()); // Symbol(id) 

console.log(id1.description);

let id3 = Symbol();
//如果在创建时没有提供 描述，那么使用description时，会返回 undefined
console.log(id3.description); // undefined 
```

symbol 类型用于创建对象的唯一标识符。

## “隐藏“属性

Symbol 允许创建对象的”隐藏“属性， 代码的任何其他部分都不能意外访问或者重写这些属性。

```js .line-numbers
const user = {
	name: 'Tom',
	age: 18
};

let id = Symbol('id');
user[id]  = 'abc';

// 如果不能拿到 id 这个变量，就不能访问到 这个Symbol
console.log(user[id]);

let user2 = {
	name: 'Tom',
	[id]: 'abc' // 
}
```