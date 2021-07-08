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

### 类式组件简写

``` jsx
class MyComponent extends React.Component{
    state = {isStudy: true}

    render(){
		const {isStudy} = this.state
		return <p onClick={this.changeStudy}>今天{isStudy?'学习了':'没学习'}</p>
	}
    
    changeStudy = ()=>{
        const isStudy = this.state.isStudy
        this.setState({isStudy:!isStudy})//这里需要调用内置方法setState更新状态，这样才会自动调用render重新渲染视图
    }
}
```

### React props

props 相当于组件或者函数的入参，组件渲染需要的差异化参数由它渲染

函数式组件应用案例：

``` jsx
function Welcome(props) {
  	return <h1>Hello, {props.name}</h1>;
}
```

类式组件应用案例：

```jsx
class Welcome extends React.Component {
  	render() {
    	return <h1>Hello, {this.props.name}</h1>;
  	}
}
```

渲染：

```jsx
const element = <Welcome name="Sara" />;
ReactDOM.render(
  	element,
  	document.getElementById('root')
);
```

### React refs

refs提供了一种访问Dom的方式，它能给组件被调用后的真实Dom做标记，这样就可以直接进行Dom操作

```jsx
class Welcome extends React.Component {
    showData = ()=>{
        const {input1} = this.refs
        alert(input1.value)
    }
    
  	render() {
    	return (
            <input ref="input1" />
            <button onClick={this.showData}>点击显示输入框内容</button>
        )
  	}
}
```

不推荐这样使用refs，因为其存在效率问题，应当使用回调形式的refs，其本质是使用ref取出dom然后挂载到组件实例自身上，形如：

```jsx
class Welcome extends React.Component {
    showData = ()=>{
        const {input1} = this
        alert(input1.value)
    }
    
  	render() {
    	return (
            <input ref={(currentNode)=>{this.input1 = currentNode}} />
            <button onClick={this.showData}>点击显示输入框内容</button>
        )
  	}
}
```

注意：如果使用回调内联的方法定义的，在更新的时候会被执行两次，第一次取得的是空对象，但是它其实无关紧要，如需避免则需要定义成类绑定的方式



