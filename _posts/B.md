<h2 align ="center">B站二面问题</h2>

其实我本来都准备去面b站的二面了，因为一面的感觉就是B站这个公司的面试难度太低了，做的事情属实没意思，好像二面也是一样的。感觉都是面经问题，好像面经背的多了就好了。下面来记录一下面试中的一些问题吧。

第一个问题：

用setTimeout 实现 setInterval（没思路呀，好像红宝书上有个这个）

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

第二个问题：前端路由的原理？以及两种实现方式的区别？

前端路由的本质是监听url的变化，匹配正确的路由规则，实现页面的更新，并且无需刷新页面。

前端路由的实现方式（两种）：

1.hash方式：



