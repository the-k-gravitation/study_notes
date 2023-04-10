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

字段初始化的顺序：
- 对于基类（还未继承任何东西的那种），在构造函数调用前初始化。
- 对于派生类，在 `super()` 后立刻初始化。

***父类构造器总是使用父类的字段*** 。

```js {.line-numbers}
class Animal { 
	name = 'animal'; 
	constructor() { 
		alert(this.name); 
	} 
}

class Rabbit extends Animal { 
	name = 'rabbit'; 
}

new Animal(); // animal 
new Rabbit(); // animal
```

对于 方法，当父类构造器在派生的类中被调用时，它会使用被重写的方法。

```js {.line-numbers}
class Animal { 
	showName() { 
	// 而不是 this.name = 'animal' 
	alert('animal'); 
	} 
	constructor() { 
		this.showName(); 
		// 而不是 alert(this.name);
	}
}
class Rabbit extends Animal { 
	showName() { alert('rabbit'); } 
} 

new Animal(); // animal 
new Rabbit(); // rabbit
```

## 静态属性和静态方法

静态方法被用于实现属于整个类的功能。它与具体的类实例无关。静态属性被用于当我们想要存储类级别的数据时，而不是绑定到实例。
它们都被用关键字 `static` 进行了标记。静态属性和方法是 `可被继承` 的。

```js {.line-numbers}
class MyClass { 
	static property = ...; 
	static method() {
	 //...
	} 
}

// 从技术上讲，静态声明与直接给类本身赋值相同：
MyClass.property = ... 
MyClass.method = ...
```