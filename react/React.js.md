一个 React 项目中，默认会安装：

- react： React 框架的核心
- react-dom： React 视图渲染的核心【基于 React 构建 WebApp（HTML 页面）】
- react-scripts： 脚手架为了让项目目录看起来干净一些，把 webpack 打包的规则以及想着的插件、Loader 等都隐藏到了 node_modules 目录下，它就是脚手架中自己对打包命令的一种封装，基于它打包，会调用 node_modules 中的 webpack 等进行处理。
- react-native： 用于构建和渲染 App
- web-vitals： 性能检测工具

## JSX

### 数据渲染规则

- `number`/ `string`： 值是啥就渲染出来啥
- `boolean`/`null`/`undefined`/`Symbol`/`BigInt`： 渲染的内容为空
- `普通对象` 不支持渲染
- `数组` 对象：把数组的每一项都分别拿出来渲染，并不是变为字符串渲染，各项之间没有逗号

## 函数组件

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

### 生命周期

## Hooks 组件

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
```

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
