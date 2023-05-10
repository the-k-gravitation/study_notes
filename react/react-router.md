## React-Router

`react-router` 用来在 `react` 中实现路由。

在 `Web` 中使用 `react-router-dom` 库。
在 移动端使用 `react-router-native` 库。

### 内置组件

`react-router-dom` 中重要的内置组件：

1. BrowserRouter

2. HashRouter

3. Route

4. Redirect

5. Link

6. NavLink

7. Switch

### 几个重要的内置对象和函数

1. history 对象

2. match 对象

3. withRouter 对象

### 路由组件与一般组件

路由组件与一般组件的区别：

1. 写法不同：
   一般组件： `<Demo />`
   路由组件：`<Route path='/demo' component={Demo}>`

2. 存放位置不同：
   一般组件：一般放在 `component` 文件夹下
   路由组件：一般放在 `pages` 文件下

3. **接收到的 `props` 不同**：
   一般组件：写组件标签时传递了什么，就能收到什么
   路由组件：会接收到 **3** 个固定的属性：`history`, `location`, `match`

**history** 中的重要方法：

1.  `function go(n)`
2.  `function goBack()`
3.  `function goForward()`
4.  `function push(path, state)`
5.  `function replace(path, state)`

**location** 中的重要属性：

1. `pathname`
2. `search`
3. `state`

**match** 中的重要属性：

1. `params`
2. `path`
3. `url`
