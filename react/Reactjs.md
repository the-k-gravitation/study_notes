一个 React 项目中，默认会安装：

- react： React 框架的核心
- react-dom： React 视图渲染的核心【基于 React 构建 WebApp（HTML 页面）】
- react-scripts： 脚手架为了让项目目录看起来干净一些，把 webpack 打包的规则以及想着的插件、Loader 等都隐藏到了 node_modules 目录下，它就是脚手架中自己对打包命令的一种封装，基于它打包，会调用 node_modules 中的 webpack 等进行处理。
- react-native： 用于构建和渲染 App
- web-vitals： 性能检测工具

## JSX

### 数据渲染规则

- `number`  /  `string`： 值是啥就渲染出来啥
- `boolean`/`null`/`undefined`/`Symbol`/`BigInt`： 渲染的内容为空
- `普通对象` 不支持渲染
- `数组` 对象：把数组的每一项都分别拿出来渲染，并不是变为字符串渲染，各项之间没有逗号

## [函数组件](./)

函数组件属于“静态”组件，即函数组件第一次渲染完毕后，组件的 View，不会随组件中的数据的变化而更新，即视图不会再更新了。

函数组件不具备状态、生命周期函数、`ref` 等内容。

```jsx {.line-numbers}
import React from 'react';

const FunctionComponent = function FunctionComponent() {
  let num = 0;
  return (
    <div>
      {num}
      <br />
      <button
        onClick={() => {
          num++;
          console.log(num); // 变量值会增加，但组件视图不会更新渲染
        }}>
        增加
      </button>
    </div>
  );
};

export default FunctionComponent;
```

在函数组件中使用 `Hooks函数` （即 `Hooks` 组件），也可以对函数组件的视图进行更新。

## 类组件

类组件属于“动态”组件。
它继承自 `React.Component` 或者 `React.PureComponent` 。

```jsx {.line-numbers}
import React from 'react';
import PropTypes from 'prop-types';

class Parent extends React.Component {
  // 属性默认值设置
  static defaultProps = {
    title: '这是一个默认标题',
    sum: 0,
  };
  // 属性规则校验
  static propTypes = {
    title: PropTypes.string.isRequired,
    sum: PropTypes.number,
  };

  // 状态
  state = {
    x: 1,
    y: 2,
  };

  // render 视图
  render() {
    let { x, y } = this.state;
    return (
      <div>
        <span>x= {x}</span>
        <span>y= {y} </span>
      </div>
    );
  }
}
```

#### setState

### 生命周期

### Lazyload

可以通过 `react` 提供的 `lazy` 函数，实现路由组件的懒加载。

```jsx
import { lazy, Suspense } from 'react';

// 使用lazy函数进行懒加载组件
const Demo = lazy(() => import('./Demo'));

// 必须对有懒加载的路由使用Suspense进行包括
<Suspense fallback={<h1>Loading...</h1>}>
  <Switch>
    <Route path="/demo" component={Demo} />
  </Switch>
</Suspense>;
```

## Hooks 组件

Hooks 只能运用到函数组件中，它就是将函数组件动态化。它本身就是函数组件。

### 基础 Hook

- `useState` 使用状态管理
- `useEffect` 使用周期函数
- `useContext` 使用上下文信息

#### useState

作用：在函数组件中使用状态，修改状态值可以让函数组件更新，类似于类组件中的 `setState` 。

基本语法：

```jsx {.line-numbers}
// state 状态的值
// setState 用于修改状态的方法
// initialState 初始的状态值
const [state, setState] = useState(initialState);
```

```jsx {.line-numbers}
import { useState } from 'react';

const Demo = function () {
  let [num, setNum] = useState(0);

  const handle = () => {
    setNum(num + 10);
  };

  return (
    <div>
      <span>{num}</span>
      <button onClick={handle}>Button</button>
    </div>
  );
};

export default Demo;
```

`useState` 中的 `setState` 函数也是异步处理的。

```jsx {.line-numbers}
import React, { useState } from 'react';

const Demo = function () {
  // 当点button时 虽然分别对xyz进行了修改，但3次修改只执行了一次Demo函数，异步处理
  console.log('render.....');

  let [x, setX] = useState(0);
  let [y, setY] = useState(0);
  let [z, setZ] = useState(0);

  const handle = () => {
    setX(x + 1);
    setY(y + 1);
    setZ(z + 1);
  };

  return (
    <div>
      <span>x: {x}</span>
      <span>y: {y}</span>
      <span>z: {z}</span>
      <button onClick={handle}>Button</button>
    </div>
  );
};

export default Demo;
```

如果想让每次修改都更新视图，则可以通过 `react-dom` 中的 `flushSync` 函数来强制进行同步更新。

```jsx {.line-numbers}
import { flushSync } from 'react-dom';

// 此时当更新x，y时，会强制更新一次视图
flushSync(() => {
  setX(x + 1);
  setY(y + 1);
});
// 更新z也会再更新一次视图
setZ(z + 1);
```

Hooks 组件有类似于 PureComponent 类组件的功能，当更新的状态值都是一样时，不去更新视图：

```jsx {.line-numbers}
import React, { useState } from 'react';
import { flushSync } from 'react-dom';
import { Button } from 'antd';

const Demo = () => {
  console.log('first');
  let [x, setX] = useState(10);

  const handle = () => {
    for (let i = 0; i < 10; i++) {
      flushSync(() => {
        setX(x + 1);
        //不会更新10次视图
        // 并且10次之后的x=11
      });
    }
  };

  return (
    <div className="demo">
      <span className="num">x: {x}</span>
      <Button onClick={handle}>Button</Button>
    </div>
  );
};

export default Demo;
```

```jsx {.line-numbers}
const handle = () => {
  for (let i = 0; i < 10; i++) {
    // 传入一个函数，则会让x每次都能加1
    setX((prev) => {
      return prev + 1;
    });
  }
};
```

useState 也可以传入一个函数，函数的参数为原本的状态：

```jsx
let [x, setX] = useState(0);

setX((preX) => preX + 1);
```

#### useEffect

`useEffect` 可以在函数组件中，使用生命周期函数。

`useEffect` 几种使用方式：

1. `useEffect(callback)`: 没设置依赖。

   - 第一次渲染完毕后，执行 `callback` ，类似于 `componentDidMount`
   - 在组件每一次更新完毕后，也会执行 `callback` ，类似于 `componentDidUpdate`

2. `useEffect(callback, [])`：设置了，但是无任何依赖
   - 只有第一次渲染完毕后，才会执行 `callback` ，类似于 `componentDidMount`

```jsx {.line-numbers}
useEffect(() => {
  // 执行一次性操作
}, []);
```

3. `useEffect(callback, [count])` 监听某个（或多个）状态的变化
   - 第一次渲染完毕会执行 `callback`
   - 当监听的状态发生变化时，也会触发 `callback`

```jsx {.line-numbers}
useEffect(() => {
  // 监听 count 状态的变化
}, [count]);
```

4. 执行清理操作，在组件卸载时执行清理操作，可以从 `effect` 函数中返回一个函数。这个函数将在组件卸载时执行。

```jsx {.line-numbers}
useEffect(() => {
  // 执行操作。

  return () => {
    // 执行清理操作。
  };
});
```

#### useContext

通过 `useContext` 可以在函数组件中，很容易就能获取创建的 `Context` 上下文中的数据。

```jsx {.line-numbers}
import React, { useContext } from 'react';
import ThemeContext from '../ThemeContext';

const VoteFooter = () => {
  // 通过useContext获取ThemeContext上下文的数据
  let { change } = useContext(ThemeContext);

  return (
    <div className="footer">
      <button
        onClick={() => {
          change('sup');
        }}>
        支持
      </button>
      <button
        onClick={() => {
          change('opp');
        }}>
        反对
      </button>
    </div>
  );
};

export default VoteFooter;
```

### 额外 Hook

- `useReducer` `useState` 的替代方案，借鉴 `redux` 处理思想，管理更复杂的状态和逻辑
- `useCallback` 构建缓存优化方案
- `useMemo` 构建缓存优化方案
- `useRef` 使用 `ref` 获取 `DOM`
- `useImperativeHandle` 配合 `forwardRef`(`ref` 转发)一起使用
- `useLayoutEffect` 与 `useEffect` 相同，但会在所有的 DOM 变更之后同步调用 `effect` 。

#### useReducer

结合 `createContext` 和 `useReducer`，可以实现在不同组件之间使用 `state` 的功能。

```jsx
import { createContext, useReducer } from "react"
import { DUMMY_PRODUCTS } from "../dummy-products.js"

export const CartContext = createContext({
  items: [],
  addItemToCart: id => {},
  updateCartItemQuantity: (productId, amount) => {},
})

function shoppingCartReducer(state, action) {
  if (action.type === "ADD_ITEM") {
    const { id } = action
    const updatedItems = [...state.items]

    const existingCartItemIndex = updatedItems.findIndex(
      cartItem => cartItem.id === id
    )
    const existingCartItem = updatedItems[existingCartItemIndex]

    if (existingCartItem) {
      const updatedItem = {
        ...existingCartItem,
        quantity: existingCartItem.quantity + 1,
      }
      updatedItems[existingCartItemIndex] = updatedItem
    } else {
      const product = DUMMY_PRODUCTS.find(product => product.id === id)
      updatedItems.push({
        id,
        name: product.title,
        price: product.price,
        quantity: 1,
      })
    }

    return {
      ...state,
      items: updatedItems,
    }
  }

  if (action.type === "UPDATE_ITEM") {
    const {
      data: { productId, amount },
    } = action
    const updatedItems = [...state.items]
    const updatedItemIndex = updatedItems.findIndex(
      item => item.id === productId
    )

    const updatedItem = {
      ...updatedItems[updatedItemIndex],
    }

    updatedItem.quantity += amount

    if (updatedItem.quantity <= 0) {
      updatedItems.splice(updatedItemIndex, 1)
    } else {
      updatedItems[updatedItemIndex] = updatedItem
    }

    return {
      ...state,
      items: updatedItems,
    }
  }

  return state
}

export default function CartContextProvider({ children }) {
  const [shoppingCartState, dispatch] = useReducer(shoppingCartReducer, {
    items: [],
  })

  function handleAddItemToCart(id) {
    dispatch({
      type: "ADD_ITEM",
      id,
    })
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    dispatch({
      type: "UPDATE_ITEM",
      data: {
        productId,
        amount,
      },
    })
  }

  const ctxValue = {
    items: shoppingCartState.items,
    addItemToCart: handleAddItemToCart,
    updateCartItemQuantity: handleUpdateCartItemQuantity,
  }

  return (
    <CartContext.Provider value={ctxValue}>{children}</CartContext.Provider>
  )
}

```

#### useCallback

#### useMemo

#### useLayoutEffect

`useLayoutEffect` 类似于 `useEffect，但是它会在` DOM 更新之后同步执行，而不是异步执行。

与 `useEffect` 不同的是， `useLayoutEffect` 的执行时机是在 `DOM` 更新之后同步执行的。这意味着，如果在 `useLayoutEffect` 中修改了 `DOM` ，用户将会看到更新后的 `DOM`，而不是更新前的 `DOM`。

由于 `useLayoutEffect` 是同步执行的，因此它可能会阻塞浏览器渲染。如果操作非常耗时，可能会导致页面卡顿。因此，建议仅在必要时使用 `useLayoutEffect`，并尽量避免在其中执行耗时操作。

#### useRef

`useRef` 能在函数组件中创建一个 `ref` 对象。

```jsx {.line-numbers}
import React, { useState, useRef } from 'react';
import { Button } from 'antd';

const Demo = () => {
  console.log('first');
  let [x, setX] = useState(0);

  const box = useRef(null);

  const handle = () => {
    setX(x + 1);
  };

  useEffect(() => {
    console.log(box.current);
  }, []);

  return (
    <div className="demo">
      <span className="num" ref={box}>
        x: {x}
      </span>
      <Button type="primary" size="small" onClick={handle}>
        Button
      </Button>
    </div>
  );
};

export default Demo;
```

#### useImperativeHandle

使用 `useImperativeHandle` 和 `useRef` 可以在子的函数组件中暴露一些属性、状态或方法给父组件。

````jsx {.line-numbers}
import React, { useState, useRef, useEffect, useImperativeHandle } from 'react';

// 函数组件需要使用React.forwardRef转发ref
const Child = React.forwardRef((props, ref) => {
  let [text, setText] = useState('Hello');

  const f = () => {};

  useImperativeHandle(ref, () => {
    // 返回的对象，会被父组件中传来的ref对象获取到
    return {
      // 将子组件中的状态值和方法暴露给父组件
      text,
      f,
    };
  });

  return (
    <div>
      <span>子的函数组件</span>
    </div>
  );
});

const Demo = () => {
  console.log('first');
  let [x, setX] = useState(0);

  const box = useRef(null);

  useEffect(() => {
    // 此时就会获取到函数子组件中的
    // useImperativeHandle 返回的对象
    console.log(box.current);
  }, []);

  const handle = () => {
    setX(x + 1);
  };

  return (
    <div className="demo">
      <Child ref={box} />
    </div>
  );
};

export default Demo;
```

## 受控组件

## 非受控组件

## Ref

使用 `Ref` 获取 DOM 元素的三种方式：

- 在元素上将 `ref` 属性设置成一个函数【推荐使用这种方式】：

```jsx {.line-numbers}
<h2 ref={(x) => (this.box = x)} className="title">
  Ref 使用函数形式
</h2>;

// 然后就可以直接能this.box来访问获取的DOM元素
console.log(this.box);
````

- 在元素上将 `ref` 属性设置成一个“名字”【已经被 deprecated，不推荐使用】：

```jsx {.line-numbers}
<h2 ref="box" className="title">
  Ref 直接使用名字形式
</h2>;

// 然后通过 this.refs.box来访问获取的DOM元素
console.log(this.refs.box);
```

- 使用 `React.createRef()` 创建一个 `ref` 对象：

```jsx {.line-numbers}
const box = React.createRef();

<h2 ref={this.box} className="title">
  Ref 直接使用名字形式
</h2>;

// 通过 ref 对象上的 current 属性来获取DOM元素
console.log(this.box.current);
```

给元素标签设置 `ref`， 可以获取对应的 DOM 元素。
给类组件设置 `ref`， 可以获取该类组件的实例对象。
对于函数组件，不能直接设置 `ref`属性，需要使用 `React.forwardRef` 来实现 `ref`的转发：

```jsx {.line-numbers}
// 将ref通过函数组件的第二个参数进行传入
const Child = function Child(props, ref) {
  return (
    <div>
      子组件
      <button ref={ref}>Submit</button>
    </div>
  );
};

// 使用React.forwardRef来对函数组件进行处理
export default React.forwardRef(Child);

// 在函数组件上进行ref设置
<Child ref={(x) => (this.box = x)} />;

console.log(this.box); // 通过this.box即可获取 button元素
```

## setState

`setState()` 在 `React18` 中是异步执行的。

语法：

```jsx {.line-numbers}
setState([partialState], [callback]);
// 或者
setState((prevState) => {
  // ...
});
```

如果提供了 `callback` 回调函数，则它会在 `componentDidUpdate` 之后执行，或者当 `shouldComponentUpdate` 返回了 `false` 时，它也会执行。

setState 还可以传递一个函数：

```jsx
setState(
  (state, props) => {
    // 在此处的函数中，可以接收到 state和props
  },
  [callback]
);
```

## 合成事件 Synthetic Event

合成事件是围绕浏览器原生事件，充当跨浏览器包装器的对象；它们将不同浏览器的行为合并为一个 API，这样做是为了确保事件在不同浏览器中显示一致的属性。

```jsx {.line-numbers}
import React from 'react';

class Demo extends React.Component {
  handle1() {
    // 未进行bind处理，此时的this为undefined
    console.log(this);
  }

  handle2(x, event) {
    // event 为合成事件：SyntheticBaseEvent
    // 通过bind进行处理的函数，可以通过在函数最后添加一个参数（event）来获取事件对象
    console.log(this, x, event);
  }

  // 推荐使用箭头函数
  // event为合成事件对象
  handle3 = (event) => {
    console.log(this, event);
  };

  // 绑定箭头函数并带传参的方式
  handle4 = (x, event) => {
    console.log(this, x, event);
  };

  render() {
    return (
      <div>
        <button onClick={this.handle1}>Button1</button>
        <button onClick={this.handle2.bind(this, 10)}>Button2</button>
        <button onClick={this.handle3}>Button4</button>
        <button
          onClick={(event) => {
            this.handle4(20, event);
          }}>
          箭头函数带参数的方式!!!
        </button>
      </div>
    );
  }
}

export default Demo;
```

## Context

一种组件间通信方式，常用于【祖组件】与【后代组件】之间的通信。
`Context` 在应用开发中一般不使用，一般都是用它来封装 `react` 插件。

使用步骤：

1. 创建 Context 容器对象：

   ```jsx
   const DemoContext = React.createContext();
   ```

2. 渲染子组件时，外面使用 DemoContext.Provider 进行包裹，通过 value 属性给后代组件传递数据：

   ```jsx
   <DemoContext.Provider value={{ a: 1, b: 2 }}>
     <子组件 />
   </DemoContext.Provider>
   ```

3. 后代组件读取数据：

   ```jsx
   // 第一种方式（仅适用于类组件）
   static contextType = DemoContext;

    // this.context 就是value中的值
   console.log(this.context);


   // 第二种方式：函数组件与类组件都可以
   <DemoContext.Consumer>
    {
      // value 就是context中的value数据
      value = (
        // 要显示的内容
      )
    }
   </DemoContext.Consumer>
   ```

## [React-Redux](./react-redux.md)

![React-Redux](./react-redux.md)

## 组件通信方式

组件间的通信方式有如下几种方式：

1. props
   - children props
   - render props
2. 消息订阅-发布
   pubs-sub 等库
3. 集中式管理
   redux、dva、mobx 等
4. Context
   生产者-消费者模式
