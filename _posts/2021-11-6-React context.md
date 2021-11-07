<h2 align ="center">React context</h2>

### API
#### React.createContexxt
创建一个Context对象，当 `React` 渲染一个订阅了这个 Context 对象的组建的，这个组件会从组件树中离自己最近的那个匹配的 Provider 中读取到当前的 Context 值。

```
const myContext = React.createContext(defaultvalue)
```

只有当组件所处的树中没有匹配到 Provider 的时候，其 `deafultValue` 参数才会生效。这有助于在不适用 `Provider` 包装组建的情况下对组件进行测试。

#### Context.Provider
每一个 Context 都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化。

Provider 接收一个 `value` 属性，传递给消费组件。一个 Provider React 组件可以和多个消费组件有关系。多个Provide也可以和