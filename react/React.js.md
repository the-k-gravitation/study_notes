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

函数组件属于“静态”组件，即函数组件第一次渲染完毕后，组件的View，不会随组件中的数据的变化而更新，即视图不会再更新了。

在函数组件中使用 `Hooks函数` （即 `Hooks` 组件），也可以对函数组件的视图进行更新。

## 类组件

类组件属于“动态”组件。