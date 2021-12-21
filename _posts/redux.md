<h1 align ="center">redux 学习</h1>

redux就那么几个核心概念，第一个就是store，redux为整个项目提供一个唯一的store，每一个组件可以使用 `store.dispatch(action)` 的方式去修改 `store`中 的数据，`action` 转交给 `reducer` 函数，`reducer` 作为一个纯函数，return一个新的`state`。`redux`提供了一个`subscribe`函数，每次更新完数据之后就去执行 `subscribe` 过的函数。

## 1、redux的设计哲学

1. single source of state

数据源头只有一个。

```
import {createStore} from "redux"

const store = createStore(reducer, preloadState, enhancer)

// createStore 的第一个参数是 reducer

export default store
```

在一个单独文件中，如放置store.js 中，这个`store`集成了`dispatch`、`getState`、`subscribe`、`replaceReducer`四个方法。

2.state is read only

`state`是只读的，就是类似于`react`中的`state`是不可以直接改变一样，在`redux`中的`state`改变的时候，我们可以去使用`dispatch(action)`的方法，去修改state。

3.Changes are made with pure function.

这个其实很好理解，对于`pure function`而言，它没有额外的影响，对于一个输入只能产生一个输出。这样的话更利于测试和预测。

## 2、redux 的基本使用

### 2.1关于store

 store 基本上我们只会去使用 `dispatch`、`getState`、`subscribe` 这三个方法第四个方法 `replaceReducer` 正常我们也不会去使用。

### 2.2构建 action

`action`其实就是一个对象

```javascript
let action = {
	type:"add"
	value:2
}
```

那么对于`redux`开发的时候我们其实就可以使用一类函数，这一类的函数用于生成一些`actions`，被称为 `action creator` 

``` javascript
const addState = (value:number) =>{
    type:"add",
    value
}
// 在这之后呢，我们就可以使用下面的方法去调用dispatch 方法了
import store from "store"

store.dispatch(addState(1))
```

### 2.3 编写和拆分 reducer

在这里举一个能够实现加减法的例子吧

```javascript
const reducer = (preState={},action) => {
	switch(action.type){
		case "add":
			return {
				...preState,
				number:preState.number + action.value
			}
		case "sub":
			return {
				...preState,
				number:preState.number - action.value
			}
        default:
            return {
                ...preState
            }
	}
}
// 这个 reducer 直接放置在 createStore中。
```

这是比较简单的情况，但是如果我们遇到比较复杂的情况的时候，我们这种方式就是不可以的了，比如说我的毕设里面，redux需要保存的数据就比较多，其中有管理登陆状态的，有的需要去管理用户的个人交易信息的，有需要管理账号信息的，还有需要管理弹窗显示信息的。各种各样的，如果这个时候我们把这些东西都放在一个reducer中，那么势必会比较混乱，对于一个reducer会频繁更改。所以可以尝试将他们分解为多个reducer，然后合并到一起。

``` javascript
import { combineReducer } from "redux"
const finalReducer = combineReducer({
    data1:reducer1,
    data2:reducer2,
})
```

这样的话，就可以对reducer进行拆分了。

