<h2 align ="center">React context</h2>

### API
#### React.createContext
创建一个Context对象，当 `React` 渲染一个订阅了这个 Context 对象的组建的，这个组件会从组件树中离自己最近的那个匹配的 Provider 中读取到当前的 Context 值。

```
const myContext = React.createContext(defaultvalue)
```

只有当组件所处的树中没有匹配到 Provider 的时候，其 `deafultValue` 参数才会生效。这有助于在不适用 `Provider` 包装组建的情况下对组件进行测试。

#### Context.Provider
每一个 Context 都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化。

Provider 接收一个 `value` 属性，传递给消费组件。一个 Provider React 组件可以和多个消费组件有关系。多个Provide也可以嵌套使用，里层的会覆盖外层的数据。

当 `Provider`的`value`值发生改变时，它内部的所有消费组件都会重新渲染。Provider及其内部 consumer都不受制于 `shouldComponentrUpdate` 函数，因此当consumer组件在其祖先组件退出更新的情况下才会更新。

新旧值之间的比较是通过Object.is 来进行比较的。

#### Class.contextType

挂载在 class 上的 `contextType` 属性会被重新赋值为一个由 `React.createContext()` 创建的 `Context ` 对象。这能让你使用 `this.context` 来消费最近 `Context` 上的那个值。你可以在任何生命周期访问到它，包括render函数中。

```
1.挂载卸载过程
	1.1 constructor
	1.2 componentWillMount
	1.3 componentDidMount
	1.4 componentWillUnmount
2.更新过程
	2.1 componentWillReceiveProps(nextProps)
	2.2 shouldComponentUpdate(nextProps,nextState)
	2.3 componentWillUpdate(nextProps,nextState)
	2.4 componentDidUpdate(preProps,preState)
	2.5 render()
```

```
export default class Index extends Component {
    render() {
        let value = this.context
        console.log(value)
        return (
            <div>
                12312
            </div>
        )
    }
}
Index.contextType = myContext;
```

值得注意的是：Function components do not support contextType. 这个contextType只有在class组建上才能使用。

#### Context.comsumer

```
<MyContext.Consumer>
  {value => /* 基于 context 值进行渲染*/}
</MyContext.Consumer>
```

这里面React 组件可以订阅到 context 变更。这能让我们在函数组件中完成订阅context。对于上层没有Provider的时候，就会调用 React.createContext函数中传入的那个defaultValue。





