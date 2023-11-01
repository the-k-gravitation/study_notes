#datatype #symbol

## 创建 Symbol 类型

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
  age: 18,
};

let id = Symbol('id');
user[id] = 'abc';

// 如果不能拿到 id 这个变量，就不能访问到 这个Symbol
console.log(user[id]);

let user2 = {
  name: 'Tom',
  [id]: 'abc', // 在字面量的对象中使用时，需要使用 计算属性 方式
};
```

## Symbol 在 for...in 中会被跳过

`Symbol`属性不会参与到 `for...in` 循环中。

```js {.line-numbers}
let id = Symbol('id');
let user = {
  name: 'Tom',
  age: 18,
  [id]: 'abc',
};

for (let key in user) {
  console.log(key); // name, age ,不会输出symbol
}

let keys = Object.keys(user); // Object.keys()会也忽略掉Symbol
console.log(keys); // ['name', 'age']
```

<font color="red">注意：</font>[Object.assign](https://developer.mozilla.org/zh/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)会同时复制字符串和 symbol 属性：

```js {.line-numbers}
let id = Symbol('id');
const user = {
  [id]: 'abc',
};

const cloneUser = Object.assign({}, user);

console.log(cloneUser[id]); // abc
```

## 全局 Symbol

在通常情况下，所有的 symbol 都是不同的，即使它们有相同的名字。
如果想要让名字相同的 Symbol 具有相同的实体， 则需要 使用 <font color="red">全局 Symbol 注册表</font> 来实现。 它可以确保访问相同描述名字的 Symbol 时，返回的都是同一个 Symbol。
使用 `Symbol.for(key)` 从<font color="red">全局 Symbol 注册表</font> 中读取或者创建(不存在时，就会创建) Symbol。

```js {.line-numbers}
const id = Symbol.for('id'); //  全局 Symbol 注册表中不存在 此 symbol对象，此时就会创建一个新的

const id2 = Symbol.for('id'); // 由于已经在 全局 Symbol 注册表 中已经存在了描述名字为“id”的 symbol，就会将其读取出来

console.log(id == id2); // true
```

可以使用 `Symbol.keyFor(symbol)` 通过 symbol 对象返回其标签名字：

```js {.line-numbers}
let s1 = Symbol.for('symbol1');

console.log(Symbol.keyFor(s1)); // symbol1

//直接通过 description就可以获取到标签名字：
console.log(s1.description);
```
