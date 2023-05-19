## React-Redux

`React-Redux` 主要用来集中管理 `react` 应用中多个组件 **共享** 的状态。

![redux](imgs/redux.png)

### Redux 的三个核心概念

#### Action

Action 动作对象，它包含 2 个属性：

- `type`: 标识属性，值为字符串，且必须为唯一，必要属性。
- `data`: 数据属性，值类型任意，可选属性。

#### Store

将 state、action、reducer 联系在一起的对象。

#### Reducer

用于初始化状态和加工状态值。
加工时，根据旧的 `state` 和 `action`， 产生新的 `state` 的 **纯函数**。

## Redux Toolkit

Redux Toolkit

## Redux DevTools 拓展
