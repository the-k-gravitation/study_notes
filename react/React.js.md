一个React项目中，默认会安装：

- react： React框架的核心
- react-dom： React视图渲染的核心【基于React构建 WebApp（HTML页面）】
- react-scripts： 脚手架为了让项目目录看起来干净一些，把webpack打包的规则以及想着的插件、Loader等都隐藏到了node_modules目录下，它就是脚手架中自己对打包命令的一种封装，基于它打包，会调用node_modules中的webpack等进行处理。
- react-native： 用于构建和渲染App
- web-vitals： 性能检测工具


## JSX

### 数据渲染规则
- `number`/ `string`： 值是啥就渲染出来啥
- `boolean`/`null`/`undefined`/`Symbol`/`BigInt`： 渲染的内容为空
- `普通对象` 不支持渲染
- `数组` 对象：把数组的每一项都分别拿出来渲染，并不是变为字符串渲染，各项之间没有逗号