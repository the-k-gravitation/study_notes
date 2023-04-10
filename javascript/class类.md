## Class 与 Function 的不同

1. 通过 class 创建的函数具有特殊的内部属性标记 [[IsClassConstructor]]: true。因此，它与手动创建并不完全相同。 与普通函数不同，必须使用 new 来调用它：

```js {.line-numbers}
class User {
  constructor() {}
}

alert(typeof User); // function
User(); // Error: Class constructor User cannot be invoked without 'new'
```

2. 类方法不可枚举。 类定义将 "prototype" 中的所有方法的 `enumerable` 标志设置为 `false` 。
3. 类总是使用 `use strict`。 在类构造中的所有代码都将自动进入严格模式。

## 计算属性名称[…]

```js {.line-numbers}
class User {
  ['say' + 'Hi']() {
    alert('Hello');
  }
}

new User().sayHi();
```
