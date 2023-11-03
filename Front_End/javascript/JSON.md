 #json #javascript

JSON 支持 object，array，string，number，boolean 和  `null`。

## JSON.stringify()

`JSON.stringify`  将对象转换为 JSON。

```js {.line-numbers}
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  spouse: null,
};

let json = JSON.stringify(student);

console.log(json); // {"name":"John","age":30,"isAdmin":false,"courses":["html","css","js"],"spouse":null}
```

JSON 编码的对象与对象字面量有几个重要的区别：

- 字符串使用双引号。JSON 中没有单引号或反引号。所以  `'John'`  被转换为  `"John"`。
- 对象属性名称也是双引号的。这是强制性的。所以  `age:30`  被转换成  `"age":30`。

JSON 是语言无关的纯数据规范，因此一些特定于 JavaScript 的对象属性会被  `JSON.stringify`  跳过。

- 函数属性（方法）。
- Symbol 类型的键和值。
- 存储  `undefined`  的属性。

```js {.line-numbers}
let user = {
  sayHi() {
    // 被忽略
    alert('Hello');
  },
  [Symbol('id')]: 123, // 被忽略
  something: undefined, // 被忽略
};

alert(JSON.stringify(user)); // {}（空对象）
```

## JSON.parse()

`JSON.parse(str, [reviver])` 将 JSON 字符串转换成 javascript 中的对象。

```js {.line-numbers}
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let obj = JSON.parse(str, function (key, value) {
  if (key === 'date') return new Date(value);
  return value;
});
```
