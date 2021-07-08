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

## React 组件

- 函数式组件

  定义一个函数，形如：

  ```jsx
  function MyComponent(){
      return <p>我是一个函数式组件</p>
  }
  ```

  需要注意的是，函数式组件的函数名首字母应当大写

- 类式组件

  定义一个类，需要继承React.Component，形如：

  ``` jsx
  class MyComponent extends React.Component{
  	render(){
  		return <p>我是一个类式组件</p>
  	}
  }
  ```

  需要注意的是类式组件必须继承React.Component，类名的首字母需要大写

### React state

即类式组件的状态，状态驱动视图

``` jsx
class MyComponent extends React.Component{
	constructor(props){
		super(props)
		this.state = {
			isStudy: true
		}
	}
	render(){
		const {isStudy} = this.state
		return <p>今天{isStudy?'学习了':'没学习'}</p>
	}
}
```

### React 组件监听事件

以点击事件onclick为例，在jsx中需要写onClick，赋值要写{函数名}的形式，例如：

``` jsx
class MyComponent extends React.Component{
	constructor(props){
		super(props)
		this.state = {
			isStudy: true
		}
	}
	render(){
		const {isStudy} = this.state
		return <p onClick={dome}>今天{isStudy?'学习了':'没学习'}</p>
	}
}
```

### React 类式组件 this 指向问题

当在类式组件里面需要写一些方法完配合组件事件来更新state时，会出现this指向问题，因为只有当实例本身调用方法才能在方法里的this拿到实例本身，类式组件的方法默认开启了严格模式，所以需要在类的构造器里预修改具体方法的this指向，例如：

``` jsx
class MyComponent extends React.Component{
	constructor(props){
		super(props)
		this.state = {
			isStudy: true
		}
        this.changeStudy = this.changeStudy.bind(this)//关键代码
	}
	render(){
		const {isStudy} = this.state
		return <p onClick={this.changeStudy}>今天{isStudy?'学习了':'没学习'}</p>
	}
    
    changeStudy(){
        const isStudy = this.state.isStudy
        this.setState({isStudy:!isStudy})//这里需要调用内置方法setState更新状态，这样才会自动调用render重新渲染视图
    }
}
```

## 