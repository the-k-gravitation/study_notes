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

## 类的继承

- 扩展一个类：`class Child extends Parent`， 这意味着 `Child.prototype.__proto__` 将是 `Parent.prototype`，所以方法会被继承。

- 重写一个 constructor，在使用 `this` 之前，我们必须在 `Child` 的 constructor 中将父 constructor 调用为 `super()`。
- 重写一个方法， 可以在一个 `Child` 方法中使用 `super.method()` 来调用 `Parent` 方法。
- 箭头函数没有自己的 `this` 或 `super`。