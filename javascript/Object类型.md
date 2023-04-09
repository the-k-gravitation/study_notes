#javascript #datatype #object

`object` 类型用于储存数据集合和更为复杂的数据实体。
通过带有可选 **属性列表** 的 **花括号{...}** 来创建对象。 一个属性就是一个键值对（key:value），其中键 key 是一个字符串（属性名），值 value 可以是任何值。

## 创建空对象

```js {.line-numbers}
let o = new Object(); // "构造函数" 的语法
let o2 = {}; // "字面量" 的语法 （通常使用字面量语法）
```

## 属性

属性的值可以是做任意类型。

```js {.line-numbers}
let user = {
  name: 'Tom',
  age: 18,
  'favorite language': 'English', // 多个词的属性名时，必须加引号
};

user.gender = 'F'; // 可以动态地添加属性

// 使用delete删除对象上的属性
delete user['favorite language']; // 对于多个词的属性引用，不能使用点号形式，必须要把整个属性名使用引用括起来
delete user.gender;
```

访问属性的方式：

```js {.line-numbers}
let user = {
  name: 'Tom',
  age: 18,
  'favorite language': 'English',
};

let name = user.name; //点符号的方式
let age = user['age'];
let favoriteLanguage = user['favorite language']; // 对于多个词的属性，只能通过中括号的方式来进行引用 ，不能使用点符号方式

// 通过中括号可以 动态地设置对象 属性
let education = 'educational background';
user[education] = 'Undergraduate';

// 点符号没办法进行动态设置属性，此时的属性名直接 为“education”，而不是想要的“educational background”
user.education = 'Undergraduate';
```

## 计算属性

#计算属性

可以通过计算属性来实现，对象的属性名从变量中动态确定。

```javascript {.line-numbers}
let fruit = prompt('买的哪种水果？'， "Apple");

let bag = {
	[fruit] = 5; // 属性名是动态读取的
}
```

```js {.line-numbers}
let fruit = 'Apple';
let bag = {
	[`{fruit}_count`] = 5;
}
```

## 属性值简写

当属性名跟变量名一样时，可以进行属性名缩写：

```js {.line-numbers}
function getUser(name, password) {
  return {
    name, // 跟 name: name 一样的效果
    password,
    //...
  };
}
```

属性名简写 也可以 与正常方式混用：

```js {.line-numbers}
let user = {
  name, // 跟 name: name 一样的效果
  age: 18,
};
```

## 属性命名

对象的属性名可以使用语言保留的关键字。
用其他类型作为属性名时，会自动转换为字符串：

```js {.line-numbers}
let obj = {
	12: 'Number'
};

console.log(obj["12"]); // Number
console.log(obj[12]); // 同样会返回 Number
console.log(obj.12); // 这样不行，会报错
```

## 属性存在性判断

### 操作符 “in”

在 javascript 中，对象中可以访问任何属性，即使属性不存在也不会报错，读取的属性不存在时，会得到 `undefined` 。

判断某个属性是否存在于对象中：

```js {.line-numbers}
let user = {
  name: 'Tom',
};

// 判断某个属性是否存在于对象中
console.log('name' in user); // true
console.log('age' in user); // false

let gender = 'gender';
console.log(gender in user); // false
```

### "for..in" 循环

遍历一个对象中所有的键(key)：

```js {.line-numbers}
let user = {
  name: 'Tom',
  age: 18,
  gender: 'F',
};

for (let key in user) {
  console.log(`Key: ${key}, Vaue: ${user[key]}`);
}
```

## 属性在对象中的顺序

在 javascript 中，属性的顺序规则：<font color="red">整数属性会被进行排序（从小到大的次序），其他属性则按照创建时的顺序进行排序</font> 。
*整数属性*表示把它转换成整数后，再转换回去，还是原来那个样子。 ”49“ 就是整数属性，”+49“ , ”2.1“ 都是非整数属性。

- 全是整数属性时，会把属性名的值对应的整数值进行从小到大进行排序：

```js {.line-numbers}
let countryCodes = {
  49: 'Germany',
  86: 'China',
  //...
  1: 'USA',
};

for (let code in countryCodes) {
  console.log(code); // 1, 49, 86 从小到大进行排序
}
```

- 当为非整数属性时，按照创建时的顺序进行排序：

```js {.line-numbers}
let user = {
  name: 'Tom',
  gender: 'F',
};
user.age = 18;

// 非整数属性按照创建时的顺序进行排序
for (let key in user) {
  console.log(key); // name, gender, age
}
```

- 混合属性时，先排序整数属性，再排序非整数属性：

```js {.line-numbers}
let user = {
  name: 'Tom',
  2: 3,
  gender: 'F',
  1: 1,
};

user.age = 18;
user['0'] = 0;

for (let key in user) {
  console.log(key); // 0， 1， 2， name, gender, age
}
```

## 对象的克隆与合并（浅复制）

#浅拷贝

对于一个对象变量，它存储的并不是”对象的值“，而是一个对值的”引用“（内存地址）。 因此，**拷贝类变量或者将其作为函数参数传递时，所拷贝的是引用，而不是对象本身**。

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,
  hobbies: ['game', 'football'],
};

console.log(user);
/*{
    "name": "Tom",
    "age": 18,
    "hobbies": [
        "game",
        "football" 
    ]
}*/

// 传递的是对象的引用，所以在函数中对对象进行修改时，外面的对象也会同样发生改变
function changeSomething(user) {
  user.hobbies.push('basketball');
  user.age = 28;
}

changeSomething(user);

console.log(user);
/*
{
    "name": "Tom",
    "age": 28,
    "hobbies": [
        "game",
        "football",
        "basketball"
    ]
}
*/
```

可以使用 <font color="red">Object.assign()</font> 方法来进行对象的”浅复制“：
语法： `Object.assign(dest, [arg1, arg2,...,argN])`

- 第一个参数 `dest` 表示目标对象
- 后面的 `[arg1, arg2,...,argN]` 是源对象。（可传递多个）
- 从第二个参数开始的所有参数的属性都被拷贝到 `dest` 对象中，并返回 `dest` 。

```js {.line-numbers}
const user = {
  gender: 'F',
};

const obj1 = { name: 'Tom' };
const obj2 = { age: 18 };
const obj3 = { gender: 'M' };

//如果被拷贝的属性名已经存在，那么它会被新的属性覆盖
Object.assign(user, obj1, obj2, obj3);

console.log(user);
/* {
    "name": "Tom",
    "age": 18,
    "gender": "M"
} 
*/
```

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,
};

// 同样也会将user中的所有属性拷贝到 一个空对象中，并返回这个新的对象
let user2 = Object.assign({}, user);
```

使用 `Object.assign` 复制对象时，如果对象中都只是 `原始类型` 的数据，没有嵌套的引用类型时，此时，复制出来的对象在进行修改时，不会相互影响。 但如果被克隆或复制的对象中有嵌套的引用对象时，此时修改嵌套的对象时数据时，就会相互影响。

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,
  hobbies: ['football'],
};

const user2 = Object.assign({}, user);

console.log(user);
/*
{
    "name": "Tom",
    "age": 18,
    "hobbies": [
        "football"
    ]
}
*/

user2.hobbies.push('basketball');

console.log(user); // 此时user的数据也发生了改变
/*
{
    "name": "Tom",
    "age": 18,
    "hobbies": [
        "football",
        "basketball"
    ]
}
*/
console.log(user2);
/*
{
    "name": "Tom",
    "age": 18,
    "hobbies": [
        "football",
        "basketball"
    ]
}
*/
```

## 深拷贝

#深拷贝 #lodash

可以 使用 `lodash` 库的 `_.cloneDeep(obj)` 来实现 ”深拷贝“：

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,
  hobbies: ['football'],
};

const user2 = _.cloneDeep(user);

user2.hobbies.push('basketball');

console.log(user);
console.log(user2);
```

## 对象方法

作为对象属性的函数 称为 `方法` 。

```js {.line-numbers}
let user = {
  name: 'Tom',
  age: 18,
  say: function () {
    console.log(`My name is ${this.name}`);
  },
  play() {
    console.log('方法的简写形式');
  },
};
```

## this

#this

### 方法中的 ”this“

在方法中为了访问该对象，可以使用 `this` 关键字。 `this` 的值就是在 **点之前** 的这个对象，即调用该方法的对象。

```js {.line-numbers}
user.say(); // 此时，say()中的this就是前面的user对象。
```

### "this" 不受限制

javascript 中的 `this` 可以用于任何函数，即使它不是对象的方法。 `this` 的值是在代码运行时 **_计算出来_** 的，它取决于代码上下文。
在 JavaScript 中，`this`  是“自由”的，它的值是在调用时计算出来的，它的值并不取决于方法声明的位置，而是取决于在“点符号前”的是什么对象。

```js {.line-numbers}
let obj1 = { name: 'Tom' };
let obj2 = { name: 'Jack' };

function doSomething() {
  console.log(this.name);
}

// 在严格模式下"use strict", 此时的this值为undefined, 所以 this.name 会报错
// 在非严格模式下，此时的this会指向全局对象，浏览器中为window对象
doSomething();

obj1.a = doSomething;
obj2.b = doSomething;

obj1.a(); // Tom , 此时的this指向obj1
obj2.b(); // Jack , 此时的this指向obj2
```

## 箭头函数

#箭头函数

箭头函数没有自己的 `this` ，在箭头函数内部访问的 `this` 都是从外部获取的。

```js {.line-numbers}
let user = {
  name: 'tom',
  say: () => {
    // 这里this，会从user中获取
    console.log(this);
  },
};
//此时，由于 user前面没有“点”的调用，所以此时的 this 指向全局对象，浏览器中为window对象
user.say();
```

```js {.line-numbers}
let user = {
  name: 'tom',
  say() {
    //此时的 this 从say()中获取，因为此处的say()为 user对象的方法，所以，this指向 user 对象
    (() => {
      console.log(this.name);
    })();
  },
};

// 此时，say() 中的 this 指向的就是 user 对象。
user.say();
```

## 构造函数

#构造函数 #new

构造函数 也是常规函数，只是对于它有 2 个共同的约定：

1. 以大写字母开头
2. 只能由 `new` 操作符来执行

```js {.line-numbers}
function User(name, age) {
  this.name = name;
  this.age = age;
}
```

当一个函数被使用 `new` 操作符执行时，它会按照以下步骤：

1. 一个新的空对象被创建，并分配给 `this`。
2. 函数体执行。通常它会修改 `this` ，为其添加新的属性。
3. 返回 `this` 的值。（如果函数中没有 return 或者 有 return 但不是返回一个对象时，此时会返回 this ；如果 return 一个对象，此时返回的对象会替换返回 this）

```js {.line-numbers}
new User('Tom', 18);

// 它会相当做如下几步：
function User(name, age) {
  // this = {} ； 一个新的空对象被创建，并分配给 `this`

  // 添加属性
  this.name = name;
  this.age = age;

  // 返回 this ，隐式返回
  // return this;
}
```

```js {.line-numbers}
function User(name) {
  this.name = name;

  // 此时返回的是一个新的对象，则不会返回 this
  return {
    name: '不返回this了',
  };
}
```

可以使用  `new.target`  属性来检查它是否被使用  `new`  进行调用：

```js {.line-numbers}
function User() {
  if (new.target === undefined) {
    // 表示没有使用new操作符来进行执行
    //....
  }
}

User(); // 没有使用 new 来执行
```

## 可选链 "?."

#可选链 #polyfills

可选链 `?.` 是一种访问嵌套对象属性的安全方式。它是最近才添加到 javascript 中的特性，旧式浏览器可能需要 `polyfills` 。

- 如果 _可选链_ `?.` 前面的值为 `undefined` 或者 `null` ， 它会停止运算并返回 `undefined` 。
- _可选链_ `?.` 是针对其前面的值成为可选值，对其后面的值不起作用。
- _可选链_ `?.` 可以用来安全地读取或者删除，但不能用于写入。

_可选链_ `?.` 语法的 3 种形式：

- `obj?.prop` -- 如果 `obj` 存在则返回 `obj.prop` ， 否则返回 `undefined`
- `obj?.[prop]` -- 如果 `obj` 存在则返回 `obj[prop]`， 否则返回 `undefined`
- `obj.method?.()` -- 如果 `obj.method` 存在则调用 `obj.method()`， 否则返回 `undefined`

```js {.line-numbers}
const user = {};
// 如果 address存在，则返回 user.address.street，否则返回 undefined
let street = user.address?.street;

let a = 0;
user?.say(a++); // 如果 没有user，则say()和a++不会执行

user.say?.(); // 如果 user.say存在，则调用，返回啥都不会发生

user?.['name']; // 如果 user中存在 name ，则返回 user['name']，否则 返回 undefined
```

## 原始值转换

通过实现一些方法，可以将对象转换成原始值。

类型转换在各种情况下有三种变体。它们被称为 `“hint”`。它们分别是：`"string"`, `"number"`, `"default"`。

默认情况下，普通对象具有  `toString`  和  `valueOf`  方法：

- `toString`  方法返回一个字符串  `"[object Object]"`。
- `valueOf`  方法返回对象自身。

```js {.line-numbers}
let user = { name: 'John' };

alert(user); // [object Object]
alert(user.valueOf() === user); // true
```

javascript 中提供了 3 个用于进行转换的方法：

1. 调用 `obj[Symbol.toPrimitivel](hint)` 如果这个方法存在的话。
2. 否则，对于  `"string"` hint：调用  `toString`  方法，如果它不存在，则调用  `valueOf`  方法（因此，对于字符串转换，优先调用  `toString`）。
3. 否则，对于其他 hint：调用  `valueOf`  方法，如果它不存在，则调用  `toString`  方法（因此，对于数学运算，优先调用  `valueOf`  方法）。

<font color="red">所有这些方法都必须返回一个原始值才能工作</font> 。

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,

  [Symbol.toPrimitive](hint) {
    return hint === 'string' ? `{name: "${this.name}"}` : this.age;
  },
};

alert(user); // hint: string --> {name: "Tom"}

/*
{
	"name": "Tom",
	"age": 18
}
*/
console.log(user);

console.log(+user); // hint: number --> 18
console.log(user + 2); // hint: default --> 20
```

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,

  toString() {
    return `{name: "${this.name}"}`;
  },
};

alert(user); // hint: string --> {name: "Tom"}

/*
{
	"name": "Tom",
	"age": 18
}
*/
console.log(user);

console.log(+user); // hint: number --> NaN
console.log(user + 2); // hint: default --> {name: "Tom"}2
```

```js {.line-numbers}
const user = {
  name: 'Tom',
  age: 18,

  valueOf() {
    return this.age;
  },
};

alert(user); // hint: string --> [object Object]

/*
{
	"name": "Tom",
	"age": 18
}
*/
console.log(user);

console.log(+user); // hint: number --> 18
console.log(user + 2); // hint: default --> 20
```

在实际使用中，通常只实现  `obj.toString()`  作为字符串转换的“全能”方法就足够了，该方法应该返回对象的“人类可读”表示，用于日志记录或调试。

## getter & setter

有两种类型的对象属性：
- 第一种是 **数据属性**。
- 第二种是 **访问器属性（accessor property）**。它们本质上是用于获取和设置值的函数，但从外部代码来看就像常规属性。

访问器属性由 “getter” 和 “setter” 方法表示。

```js {.line-numbers}
let user = { 
	name: "John", 
	surname: "Smith", 
	
	get fullName() { 
		return `${this.name} ${this.surname}`; 
	}, 
	set fullName(value) { 
		[this.name, this.surname] = value.split(" "); 
	}
};
```

```js {.line-numbers}
function User(name, birthday) { 
	this.name = name; 
	this.birthday = birthday; 
	// 年龄是根据当前日期和生日计算得出的 
	Object.defineProperty(this, "age", { 
		get() { 
			let todayYear = new Date().getFullYear(); 
			return todayYear - this.birthday.getFullYear();
		 } 
	});
}
```


一个属性要么是访问器（具有 `get/set` 方法），要么是数据属性（具有 `value`），但不能两者都是。

## Prototype 

在 JavaScript 中，所有的对象都有一个隐藏的 `[[Prototype]]` 属性，它要么是另一个对象，要么就是 `null`。

- 通过 `[[Prototype]]` 引用的对象被称为“原型”。
- 如果我们想要读取 `obj` 的一个属性或者调用一个方法，并且它不存在，那么 JavaScript 就会尝试在原型中查找它。
- 写/删除操作直接在对象上进行，它们不使用原型（假设它是数据属性，不是 setter）
- 如果我们调用 `obj.method()`，而且 `method` 是从原型中获取的，`this` 仍然会引用 `obj`。因此，方法始终与当前对象一起使用，即使方法是继承的。
- `for..in` 循环在其自身和继承的属性上进行迭代。所有其他的键/值获取方法仅对对象本身起作用。

```js {.line-numbers}
let animal = { eats: true }; 

let rabbit = { 
	jumps: true, 
	__proto__: animal 
}; 

for(let prop in rabbit) { 
	let isOwn = rabbit.hasOwnProperty(prop); 
	if (isOwn) { 
		alert(`Our: ${prop}`); // Our: jumps 
	} else { 
		alert(`Inherited: ${prop}`); // Inherited: eats 
	} 
}
```


