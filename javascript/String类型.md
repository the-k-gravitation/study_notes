#datatype #string

在 javascript 中， 字符串是不可更改的。
有 3 种表示字符串的方式：

- 双引号： "Hello,World"。
- 单引号： 'Hello,World'。
- 反引号： \`Hello,World\`。

双引号和单引号没有什么区别。 `反引号`是 **功能扩展** 引号，通过它可以将变量或者表达式包装在`${...}`中，嵌入到字符串，方便字符串的操作。

```js {.line-numbers}
let firstName = 'Tom';
let lastName = 'Wu';
let fullName = `${firstName} ${lastName}`; // fullName = ："Tom Wu"

console.log(`1 + 2 = ${1 + 2}`); //输出：1 + 2 = 3
```

可以使用 `for .. of` 遍历字符：

```js {.line-numbers}
for (let char of 'Javascript'){
	console.log(char);
}
```

在 javascript 中没有 character 类型，一个字符串可以包含零个（为空）、一个或者多个字符。

## 字符串转换

可以调用`String(value)`来将`value`转换为字符串类型

```js {.line-numbers}
let v = true;
let vStr = String(v); // "true"

v = null;
vStr = String(v); // "null"
```

 