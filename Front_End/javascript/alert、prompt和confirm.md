 #javascript

alert、prompt 和 confirm 为与用户交互的 3 个浏览器的特定函数。它们弹出的窗口称为“**模态窗(modal)**”， 它们会暂停脚本的执行,并且用户不能与页面的其他部分进行交互，直到模态窗口关闭。

它们弹出的模态窗口：

- 模态窗口的确切位置由浏览器决定。通常在页面中心。
- 窗口的确切外观也取决于浏览器。我们不能修改它。

## alert

用来弹出一些提示信息。

```js {.line-numbers}
alert('Hello, World.');
```

## prompt

`prompt` 浏览器会显示一个带有文本消息的模态窗口，还有 `input` 框和确定/取消按钮。

```js {.line-numbers}
let result = prompt(title, [default]);
```

接收两个参数：

- `title`
  显示给用户的文本字符串
- `default`
  可选的第二个参数，指定 input 框的初始值。

```js {.line-numbers}
let result = prompt('abc', 123);

console.log(typeof result);
console.log(result === null);

// 按取消键： result 为 object 类型，值为 null
// 按确定键： result 为 string 类型，值为 输入的值或者初始值
```

在 IE 浏览器中，如果未提供第二个参数，它会默认将“undefined”插入到 prompt，所以最好每次都为 prompt 函数提供第二个参数。

## confirm

`confirm` 弹出显示信息等待用户点击确定或取消。点击确定返回 `true` ，点击取消或按下 Esc 键返回 `false` 。

```js {.line-numbers}
let result = confirm('Are you ok?');
```
