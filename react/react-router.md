## React-Router

`react-router` 用来在 `react` 中实现路由。

在 `Web` 中使用 `react-router-dom` 库。
在 移动端使用 `react-router-native` 库。

### 内置组件

`react-router-dom` 中重要的内置组件：

1. BrowserRouter

   `BrowserBouter` 使用的是 `H5` 中的 `history API`，不兼容 `IE9` 及以下版本。
   `BrowserBouter` 的路径中没有”#“。
   刷新后对路由 `state` 参数没有任何影响。

2. HashRouter

   `HashRouter` 使用的是 URL 的哈希值。
   `HashRouter` 的路径中**包含**”#“。
   刷新后,可能会导致路由 `state` 参数丢失。

3. Route

4. Redirect

5. Link

6. NavLink

   `NavLink` 可以实现路由链接的高亮，可以通过 activeClassName 来指定“高亮”的样式名，

7. Switch

### 几个重要的内置对象和函数

1. history 对象

2. match 对象

3. withRouter 函数

`withRouter` 可以让一般组件拥有路由组件中的`history`, `location`, `match`。

```jsx
import { withRouter } from 'react-router-dom';

class Demo extends Component {}

export default withRouter(Demo);
```

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

1. `function go(n)`
2. `function goBack()`
3. `function goForward()`
4. `function push(path, state)`
5. `function replace(path, state)`

**location** 中的重要属性：

1. `pathname`
2. `search`
3. `state`

**match** 中的重要属性：

1. `params`
2. `path`
3. `url`

### 向路由组件传递参数

1. `params` 参数

   - 路由链接中携带参数：

     ```jsx
     <Link to={`/user/detail/${user.id}`}>用户信息</Link>
     ```

   - 注册路由中声明接收参数：

     ```jsx
     <Route path="/user/detail/:id" component={UserDetail} />
     ```

   - 路由组件中接收参数：
     在路由组件中的 `props` 属性中的 `match` 属性中会有传递过来的参数，并以对象的形式存储在其中。

     ```jsx
     const { id } = this.props.match.params;
     ```

2. `search` 参数

   - 路由链接中通过在“?”号后面携带参数：

     ```jsx
     <Link to={`/user/detail?id=${user.id}`}>用户信息</Link>
     ```

   - 注册路由中无需声明接收参数

     ```jsx
     <Route path="/user/detail" component={UserDetail} />
     ```

   - 路由组件中接收参数：
     在路由组件中的 `props` 属性中的 `location` 属性中的 `search` 属性会有传递过来的参数，如：“?id=001&name=abc”

     ```jsx
     // 借助querystring库进行解析
     import qs from 'querystring';

     const { search } = this.props.location;
     // 需要将第一个字符“？”号去掉才能进行解析，qs.parse 解析之后，以对象的形式返回
     const { id } = qs.parse(search.slice(1));
     ```

3. `state` 参数

- 路由链接：

  ```jsx
  <Link
    to={{
      pathname: '/user/detail',
      state: { id: '01' },
    }}>
    用户信息
  </Link>
  ```

- 注册路由中无需声明接收参数

  ```jsx
  <Route path="/user/detail" component={UserDetail} />
  ```

- 路由组件中接收参数：
  在路由组件中的 `props` 属性中的 `location` 属性中的 `state` 属性会有传递过来的参数，并以对象的形式存储在其中。

  ```jsx
  const { id } = this.props.location.state;
  ```

**注意**：由于不在 path 中传递参数，如果清空浏览器缓存，则会没法取到 state 参数。
