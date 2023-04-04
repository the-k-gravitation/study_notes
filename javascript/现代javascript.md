# JavaScript 基础知识

## Hello,World!

![script标签](script标签.md)

## 代码结构

![代码结构](./代码结构.md)

## 变量

![变量](./变量.md)

## alert、prompt 和 confirm

![alert、prompt 和 confirm](./alert、prompt和confirm.md)

## 数据类型

![数据类型](./数据类型.md)

## 数组 Array

![[数组Array]]

## Map & Set

![[Map_Set]]

## 解构赋值

解构赋值可以简洁地将一个对象或数组拆开赋值到多个变量上。

- 解构对象的完整语法：

```js {.line-numbers}
let {prop : varName = default, ...rest} = object
```

这表示属性  `prop`  会被赋值给变量  `varName`，如果没有这个属性的话，就会使用默认值  `default`。没有对应映射的对象属性会被复制到  `rest`  对象。

- 解构数组的完整语法：

```js {.line-numbers}
let [item1 = default, item2, ...rest] = array
```

数组的第一个元素被赋值给  `item1`，第二个元素被赋值给  `item2`，剩下的所有元素被复制到另一个数组  `rest`。

- 从嵌套数组/对象中提取数据也是可以的，此时等号左侧必须和等号右侧有相同的结构。

```js {.line-numbers}
let options = { title: 'Menu' };

let { width: w = 100, height: h = 200, title } = options;

let options = { title: 'Menu', width: 100, height: 200 };

// { sourceProperty: targetVariable }
let { width: w, height: h, title } = options;
```

## 基础运算符，数学运算

![基础运算符，数学运算](./基础运算符，数学运算.md)

## 值的比较

![值的比较](./值的比较.md)

## 逻辑运算符

![逻辑运算符](./逻辑运算符.md)

## 条件语句

![条件语句](./条件语句.md)

## 循环语句

![循环语句](./循环语句.md)

## 函数 Function

![函数Function](./函数Function.md)

## JSON

JSON 支持 object，array，string，number，boolean 和  `null`。

### JSON.stringify()

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

### JSON.parse()

`JSON.parse(str, [reviver])` 将 JSON 字符串转换成 javascript 中的对象。

```js {.line-numbers}
let str = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

let obj = JSON.parse(str, function (key, value) {
  if (key === 'date') return new Date(value);
  return value;
});
```
