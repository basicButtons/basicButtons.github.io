<h2 align ="center">B站二面问题</h2>

其实我本来都准备去面b站的二面了，因为一面的感觉就是B站这个公司的面试难度太低了，做的事情属实没意思，好像二面也是一样的。感觉都是面经问题，好像面经背的多了就好了。下面来记录一下面试中的一些问题吧。

### 第一个问：用setTimeout 实现 setInterval（没思路呀，好像红宝书上有个这个）

```
function mySetInterval(fn,delay){
	function interval(){
		setTimeout(interval,delay)
		fn()
	}
	let timer = setTimeout(interval(),delay)
	return timer
}


function mySetInterval(fn, delay, timer = {timer:null}) {
    function interval() {
        timer.timer = setTimeout(interval, delay)
        fn()
    }
    timer.timer = setTimeout(interval, delay)
    return timer
}
```

### 第二个问题：前端路由的原理？以及两种实现方式的区别？

前端路由的本质是监听url的变化，匹配正确的路由规则，实现页面的更新，并且无需刷新页面。

前端路由的实现方式（两种）：

> 传统的路由指的是后端路由，路由的意思就是指路，前端发给后端一个url，也就是通向某个页面的地址，后端服务器根据这个地址找到对应的页面，然后把该页面文件发给前端，前端接收到在展示给用户。
>  对于 Vue 这类渐进式前端开发框架，为了构建 **SPA（单页面应用）**，需要引入前端路由（因为当 url 发生改变，只是表明页面组件排列组合的方式变了，并不需要向后端发送请求重载页面。），这也就是 vue-router 存在的意义。
>  前端路由的核心，就在于——**改变视图的同时不会向后端发出请求**。
>
> 前端路由是不同的url对应不同的组件排列组合方式，但是浏览器并不知道运行的是SPA，他还默认为是传统的web应用——不同页面对应不同html。所以当你的url改变时，浏览器依然会向新的url发起请求，但这是我们不希望浏览器做的。
>  我们想要做到改变路由的同时不会向后端发出请求。

1.hash方式：

**hash** —— 即地址栏 URL 的 `#` 符号（此 hash 不是密码学里的散列运算）。

- #表示网页中的一个位置，
- 代表网页中的一个位置。其右边的字符，就是该位置的标识符。比如，
   `http://www.example.com/index.html/#/print` 就代表网页 index.html 的 print 位置。浏览器读取这个 url 后，
   会自动将 print 位置滚动至可视区域。中间问道如何直接跳转到某个id元素处，那么就是直接在url后面加上#id就可以跳转到了然后对于JS方法的话：window.location.hash = "#abc";
- 它的特点在于对于，虽然url改变了，但是不会去发起HTTP请求，不会对后端发起请求，因此hash改变不会引起页面的重新加载。
- 如何读取到hash值： windows.localtion.hash可以读取到#后面的值，读取的时候，可以判断页面状态是否改变。
- 写入时，则会在不重载网页的前提下，创造一条访问历史记录。每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用"后退"按钮，就可以回到上一个位置。这对于ajax应用程序特别有用，可以用不同的#值，表示不同的访问状态，然后向用户给出可以访问某 个状态的链接。

2.histoy方式

对于第二种路由呢，这两个方法应用于浏览器的历史记录栈，在当前已有的 `back`、`forward`、`go` 的基础之上，它们提供了对历史记录进行修改的功能。只是当它们执行修改时，虽然改变了当前的 URL，但浏览器不会立即向后端发送请求。

#### hash和history模式的对比

一般情况下 hash和history都可以，但是还有有一些具体上的差异的。

- `pushState()` 设置的新 URL 可以是与当前 URL 同源的任意 URL；而 `hash` 只可修改 `#` 后面的部分，因此只能设置与当前 URL 同文档的 URL；
- `pushState()` 设置的新 URL 可以与当前 URL 一模一样，这样也会把记录添加到栈中；而 `hash` 设置的新值必须与原来不一样才会触发动作将记录添加到栈中；

