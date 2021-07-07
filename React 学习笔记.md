# React 学习笔记

## React 是什么

React 是一个用于构建用户界面的 JavaScript 库

React 没有封装其他例如数据请求的库，只负责页面渲染

## React 高效的原因

使用了虚拟 DOM 技术

使用 DOM Diffing 算法进行最小差异的界面重绘

## 资源引入

``` html
<!--核心库-->
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<!--用于支持React操作dom-->
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
<!--用于支持jsx-->
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

## JSX

React 定义的一种 JS 的扩展语法

### JSX 语法规则

- 定义虚拟DOM时不需要写引号
- 标签引入javascript表达式时要用{}
- 写类名不能用class，要用className
- 内联样式要用style={{key:value,key:value}}的形似去写
- 只能有一个根标签
- 标签必须闭合，例如\<br/\>
- 标签首字母
  - 小写时必须保证html有这个标签，没有则会报错
  - 大写时必须定义为组件才可以使用

