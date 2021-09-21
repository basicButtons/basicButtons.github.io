<h1 align="center">JS面试问题准备</h1>

1.js的数据类型有哪些？以及这么去判断这些类型？能画一下他们的内存图吗？

```
js数据类型分为两种一种是基本数据类型，一种是引用数据类型，基本数据类型包含了null undefined string number boolean ES6中引入的symbol还有ES10中引入的Bigint，symbol主要是为了保证唯一性，这样的话就没有人能够覆盖你写的对象的属性。bigint主要是解决超出js原来数字范围限制的一些问题。

引用数据类型包含了 object 当然function 和 array都是特殊的object



类型判断的，首先可以使用typeof，instanceof、object.prototype.tostring.call()、constructor函数。



栈是用来存储基本数据类型的，堆是用来存储引用数据类型的。这两种数据类型存储的位置不一样，基本数据类型在栈中大小固定，占用空间小，所以被放在栈中。引用数据类型，大小不固定，如果存放在栈中容易引发性能问题，但是引用数据类型在栈中存放了引用数据类型的地址指针，当解释器运行到该处的时候，就可以堆内存上寻找相应的内容。

```



2.js有什么内置对象吗？

```
js 中的内置对象主要指的是在程序执行前存在全局作用域里的由 js 定义的一些全局值属性、函数和用来实例化其他对象的构造函
数对象。一般我们经常用到的如全局变量值 NaN、undefined，全局函数如 parseInt()、parseFloat() 用来实例化对象的构
造函数如 Date、Object 等，还有提供数学计算的单体内置对象如 Math 对象。
```



3.undefined 和 undecleared的区别，null 和 undefined的区别

```
undefined 指的是未被定义，但是已经被声明了，但是undecleared是指没有声明
null指的是指向一个空对象，typeof的时候也会反悔object，包括说object.prototype.__proto__ 就是一个null也就是一个空对象，但是undefined就是没有声明的一个东西
```



4.原型、原型链

```
首先说原型，对于每一个构造函数都有一个属性prototype指向一个对象，这个对象就叫做构造函数的显式对象，显式对象有一个属性constructor指向构造函数，这个构造函数每次创建一个对象之后，这个对象就有一个属性__proto__指向构造函数的函数对象，也叫做该新创建对象的隐式原型。对于每一个由该构造函数创建的对象都可以访问其隐式原型上的属性、或者方法，这就是原型。
原型链的话就是说，对于对象而言在访问其属性或者方法的时候如果没有改属性或者方法就可以去其隐式原型上去找，同时其隐式原型也是一个对象，当其隐式原型上也没有的时候，我们就去其隐式原型的隐式原型上去找，这样一次次去迭代，这样就形成了原型链，知道object.prototype.__proto__ 这个时候原型链就到了终点。
```



5.JS中获取原型的方法

```
p.__proto__
p.constructor.prototype
Object.getPrototypeOf(p)
```



6.其他值到字符串的规则，

```
1.null 和 undefined 就是直接转换 "null" "undefined"
2.Boolean 数据类型转化为 "true" 和 "false"
3.number 转化为数据类型，但是太大的时候我们就会将其转化为一些指数形式
4.对于普通的对象而言返回的就是[Object object],但是对于 function而言就是返回function的函数题，对于array的话就是将各个item用,链接到一起
```



7.其他类型转换为number的规则：

```
说一下为false的一些值
undefined null 0 Nan false
```



8.{} 和 [] valueOf 和 tostring方法的返回值：

```
{} 的 valueOf 结果为 {} ，toString 的结果为 "[object Object]"

[] 的 valueOf 结果为 [] ，toString 的结果为 ""
```



9.+什么时候用来做字符串的连接符号，什么时候用来计算？

```
简单来说就是，当两个操作数中任意一个为字符串的时候，那么就是字符串的链接符号，只有当两个操作数字都是数字的时候才是用作加号。
```



10.如何将浮点数点左边的数每三位添加一个逗号，如 12000000.11 转化为『12,000,000.11』?

```
function format(number){
 return number.tolocalString("en")
}
```



11.常用的正则表达式

```
//匹配16进制的rgb色彩
var regex = /^([0-9A-Fa-f]{6}|[0-9A-Fa-f]{3})$/g
//匹配日期，如 yyyy-mm-dd 格式
var regex = /^[1-9]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[1-2][0-9]|3[0-1])$/g
// （3）匹配 qq 号
var regex = /^[1-9][0-9]{4-9}$/g
//   手机号码正则
var reg = /^1\d{9}$/
```



12.数组随机排序

```
arr.sort(()=>{return Math.random()-0.5})

function randomSort(arr){
	var res = []
	while(arr.length > 0){
		let randomIndex = Math.floor(Math.random() * arr.length)
		res.push(arr[randomIndex])
		res.splice(randomIndex,1)
	}
	
	return res
}
```



13.继承的实现方式（参考红宝书）

```
// 1.原型链继承：
function superType(){
	this.property = ture
}
superType.prototype.getSuperProperty = function(){
	console.log(this.property)
}
function subType(){
	this.subproperty = false
}
subType.prototype = new superType()
subType.property.getSubProperty=function(){
	console.log(this.subproperty)
}
let sub = new subType()
sub.getSubProperty()
// false

缺点：1.如果原型中包含了引用值，那么我们一个subtype的实例修改了这个引用值那么所有的实例的该引用值都会被修改。
		2.没有办法在不影响所有对象的情况下，给超类传递参数。

2.借用构造函数：该方法解决了原型链中不能单独给一个对象传递给超类参数，但是问题确实，失去了和超类原型的联系，子类中没有办法访问父类上面的方法和属性。

3.组合继承：就是将一二两种方法组合到一起，子类的原型还是超类的实例，但是在子类的构造函数中还是会去调用超类的构造函数，这样构造函数实际上在子类实例的创建过程中被调用了两遍，而且多出来一些重复的属性或者方法。

4.原型式继承：这个是类似于Object.create(object) 这个方法问题是跟原型链基本相似。
5.寄生式继承：
let person = {
	friends:["shelby","Court","Van"],
	name:"Nicholas"
}
function createAnother(obj){
		let clone = object(obj)
		clone.sayHi = function(){
				console.log("hi")
		}
}
let anotherPerson = createAnother(person)
anotherPerson.sayHi()
//Hi
这个方法的问题就是没有办法复用函数，也就是说每一个创建的对象都有一个函数

6.寄生式组合继承
function inheritPrototype(subtype,suptype){
		let prototype = new suptype()
		prototype.constructor = subtype
		subtype.prototype = prototype
}
fucntion suptype(name){
		this.name = name
		this.colors=["red","blue","green"]
}
function subtype(){
		suptype.call(this)
}
寄生式组合继承避免了supertype被调用两次的问题，同时也直接将原型链也保留了下来.
```



14.作用域与作用域链 instanceOf 工作原理

```
首先讲作用域：作用域是指js中的变量的作用范围，对于js而言var变量是函数作用域，对于let 或者 const而言来说是块级作用域。
再讲作用域链：就是js中变量的访问方式，当我们调用一个变量的时候，我们在当前作用域中找不到的时候，我们就去其父作用域中去找，如果父级作用域找不到时候，就去父作用域的父作用域中去找，直到找到，最后一个父作用域为全局作用域。这个时候的问题就是如何确定父作用域，因为作用域是在函数定义的时候确定的，所以说父作用域是其在函数的父函数所对应的作用域。

function instanceOf(left,right){
		let proto = left.__proto__
		prototype = right.prototype
		while(ture){
				if(!proto) return false
				if(proto === prototype) return true
				proto = proto.__proto__
		}
}
```



15.this指向问题

```
1.首先一般函数而言，this指向为全局变量
2.方法调用的时候，就是指向调用函数的那个对象。
3.构造函数的时候，指向返回的那个new 对象
4.()=> this指向箭头函数定义处的this
5.call,apply bind 来修改this指向。
```



16.手写call apply bind 函数

```
call函数
Function.prototype.mycall=function (thisarg, ...args){
		let context
		if(typeof thisarg === "object"){
			context = thisarg || window
		}else{
			context = Objecy.create(null)
		}
		context.fn = this
		return context.fn(...args)
)

apply函数
Function.prototype.myapply = function(thisarg,argsList){
		let context
		if(typeof thisarg === "object"){
				context = thisarg||window
		}else{
				context = object.create(null)
		}
		context.fn = this
		return context.fn(..argsList)
}

bind函数
Function.prototype.mybind = function(thisarg,...args){
		let context;
		if(typeof thisarg === "object"){
			context = thisarg||window
		}else{
			context = object.create(null)
		}
		let self = this
		return function(...newargs){
				self.call(context,...args,...newargs)
		}
}
```



17.什么是DOM和BOM？

```
DOM 指的是文档对象模型，它指的是把文档当做一个对象来对待，这个对象主要定义了处理网页内容的方法和接口。

BOM是对 Browser Object Model 指的是浏览器对象模型，它指的是把浏览器当作一个对象去使用。BOM的核心是window，window有两重身份一个是BOM用来包含浏览起的一些东西，比如history，location、screen等，同时window又是全局对象，document也是window上的一个属性。
```



18.写一个通用的事件侦听器函数。

```
// 这个方法并没有完全解决所有不一致的问题，比如说，我们在IE中监听函数的this指向为window，但是对于别的浏览器而言就是该dom对象。
// 还有就是这方法没有解决，IE浏览器中attachEvent方法函数执行的顺序与增加的顺序相反的问题，对于正常的浏览器而言就是相同顺序。
const EvenUtils = {
		addEvent:function(element,type,handle){
				if(element.addEventListener){
						element.addEventListener(type,handle)
				}
				else if(element.attachEvent){
						element.attachEvent("on"+type,handle)
				}
				else{
						element["on"+type] = handle
				}
		},
		removeEvent:function(element,type,handle){
				if(element.removeEventListener){
						element.removeEventListener(type,handle)
				}
				else if(element.detachEvent){
						element.detachEvent("on"+type,handle)
				}else{
						element["on"+type] = null
				}
		},
		getEvent: function(event){
				return event|| window.event
		},
		getTarget: function(event){
				return event.target || event.srcElement
		},
		stopPropagation: function (event){
				if(event.propagation){
						event.propagation()
				}else{
						event.cancelBubble = true
				}
		},
		preventDefault : function (event){
				if(event.preventDefault){
						event.preventDefault()
				}else{
						event.returnValue = false
				}
		}
		//对于后三种方法都是要先利用getEvent获取到事件之后才可以进行的。
}
```



19.三种事件机制

```
事件是用户操作网页时发生的交互动作或者网页本身的一些操作，现代浏览器一共有三种事件模型。
DOM0 DOM0是没有冒泡机制存在的，但是所有的浏览器基本上都支持冒泡，它处理事件的形式就是直接给这个节点添加onclick function，移除函数的时候就将onclick设置为null。

DOM2 DOM2中事件分为两个阶段，一个是捕获阶段，事件处理阶段，一个是冒泡阶段，然后使用addEventListener，来进行事件监听，第三个参数true表示监听捕获阶段，false表示监听冒泡阶段。

IE事件机制 IE只有事件处理阶段和冒泡阶段，attachEvent来新增事件监听，用detachEvent来去除事件监听，然后IE的当对于一个node增加多个事件监听函数的时候，处理顺序与增加的顺序相反。
```



20.事件委托。

```
事件委托是利用事件的冒泡机制，在父节点上可以获取到事件发生的节点，然后做出相应的处理。
这样就可以不在每一个节点上就绑定函数，只需要在父节点上绑定一个监听函数就可以达到预期的目的，从而可以节省内存。
```



21.闭包

```
闭包就是能够在函数内部，使用另外一个函数内部变量的函数。最常用的构建闭包的方式就是我们在一个函数中再构建一个函数，内部函数利用到外部函数的变量，这样就形成了闭包。
闭包最常用的最用，第一个就是形成私有变量，第二个就是在内存中永远保存变量值（比如防抖、节流）。
```



22.防抖、节流

```
function debounce(fn,delay){
		let timer
		return function(){
				if(timer){
						clearTimeOut(timer)
						timer = setTimeOut(fn,delay)
				}else{
						timer = setTimeOut(fn,delay)
				}
		}
}
function throttle(fn,delay){
		let timer
		return function(){
				if(!timer){
						timer = setTimeOut(()=>{
								fn()
								clearTimeOut(timer)
						},delay)
				}
		}
}
```



23对象构建的方法 与 new的工作原理

```
对象的构建方法：
let littleDog
1.工厂函数的形式：
function dog(){
		let o = new Object()
		o.some = "123"
		return 0
}

littleDog = dog()
工厂函数的问题是，工厂函数虽然可以创建多个类似的对象，但是我们没有办法去确定每一个创建出来的object的类型。

2.构造函数的形式
function dog(){
		this.name = "123"
		this.bark = ()=>{
				console.log("wang wang wang!")
		}
}
littleDog = new dog()

对于构造函数的问题就是，对于我们所使用构造函数创建的每一个对象，他们都会包含一些相同的对象和属性，这样的话就造成了一定的冗余。

3.原型方法
function dog(){}
dog.prototype.name = "123"
littledog = new dog()

4.组合方式，将以上两种方法组合到一起。

new的工作原理
function _new(func,...args){
		let res = {}
		func.call(res,...args)
		res.__proto__ = func.prototype
		return res||{}
}
```



24.JSON的理解

```
json是一种轻量级的数据传输格式，可以表达复杂的数据结构，主要是对象。

虽然json对js的支持不错但是还是有一些问题，比如说json中不能有函数，NaN。
JSON提供了两个方法，JSON.stringify 和 JSON.parse 这两个方法可以用于对象的深拷贝，但是如果对象中包含了函数或者NaN的话，就不可以了，因为我们在这样两步操作之后，就会直接失去这些属性。
```



25.深浅拷贝问题：

```
深拷贝：
function deepCopy(obj){
		let res = {}
		for(let key in obj){
				if(obj.hasOwnProperty(key)){
						if(typeof obj[key] === "object"){
								res[key] = deepCopy(obj[key])
						}else{
								res[key] = obj[key]
						}
				}
		}
}
```



26.js延迟加载的方法

```
script 标签 async 和 defer的区别：
async是异步加载js，然后js一旦加载完毕之后就回去执行，但是defer却是这个属性会让脚本的加载与文档的解析同步解析，然后在文档解析完成后再执行这个脚本文件，这样的话就能使页面的渲染不被阻塞。多个设置了 defer 属性的脚本按规范来说最后是顺序执行的，但是在一些浏览器中可能不是这样。
```



27.ajax 与Promise封装

```
let xhr = new XMLHttpRequest()
xhr.open("GET","/some",true)
xhr.onreadystatechange= function(){
    if(this.readystate !== 4){
        return 
    }
    else{
        handle(xhr.response)
    }
}
xhr.send()

function getJSON(url){
  let promise = new Promise((resolve,reject)=>{
      let xhr = new XMLHttpRequest()
      xhr.open("GET",url,false)
      xhr.onreadystatechange = function(){
          if(this.readyState !== 4){
              return 
          }else{
              if((xhr.status >= 200 && xhr.status<300)||xhr.status === 304){
                  resolve(xhr.response)
              }else{
                  reject(xhr.statusText)
              }
          }
      }
      xhr.send()
  })
  return promise
}
```



28.浏览器的缓存机制：

```
web缓存的作用：
1.可以减少宽带消耗
2.减小服务器压力
3.减少个人的延迟

浏览器先向代理服务器发起web请求，再将请求转发到源服务器。它属于共享缓存，所以很多地方都可以使用其缓存资源，因此对于节省流量有很大作用。

浏览器缓存是将文件保存在客户端，在同一个会话过程中会检查缓存的副本是否足够新，在后退网页时，访问过的资源可以从浏览器缓存中拿出使用。通过减少服务器处理请求的数量，用户将获得更快的体验

缓存的处理步骤：
1.接受请求报文
2.解析各种头部和url
3.查询是否有副本可以使用
4.新鲜程度验证
5.创建响应
6.发送和记录日志

客户端的控制头部设置：
1.Pragma:no-cache(这个被以后的头部替代了)
2.Cache-control:no-cache no-store max-age 
// 3.if-modify-since
// 4.if-None-Match
//	3,4	主要用于协商缓存。

响应头部：
1.ETag:
2.Last-modify
3.Expires
4.cache-control
```



29.同源策略与跨域请求

```
同源策略：
同源是指：两个域的协议，主机名（ip），端口都必须相同。否则都不能说是一个域。
同源限制主要是限制了以下三个方面：
1.js不能访问其他域下的cookie、localstorage、indexDB
2.js不能操作其他域下的DOM
3.ajax不能发送跨域请求

同源策略也主要是为了保护用于的安全，他是对js的一种限制，但是并不是对浏览器的一种限制，对于img和script标签却没有这种限制。

解决跨域问题：
1.jsonp
jsonp主要是利用script标签没有收到同源策略的限制，我们利用script标签对另外一个域发送get请求。
<script>
		var script = document.createElement("script")
		scrript.type = "text/javascript"
		
		script.src = url+"?callback = "
		document.head.append(script)
		
		function callback(res){
				console.log(res.stringify(res))
		}
</scripts>
// 切记jsonp只能发送get请求。

2.document.domain + iframe 进行跨域
此方案只能用于主域名相等，子域名不同的时候
实现原理：通过设置document.domain 为基础主域，这样就可以使他们在同一个域上，这样就可以实现跨域了。
2.1父窗口上：
<iframe id = "iframe" src = 另外一个地址></iframe>
<script>
    document.domain = 'domain.com';
    var user = 'admin';
    let ifr = document.getElementById("iframe"),
    doc = ifr.contentDocument
    // 这个时候doc就是子窗口的dom结构。
    
</script>

2.2子窗口
<script>
		document.domain = 'domain.com'
		alert(window.parent.user)
</script>

3.
```



30.cookie

```

```



32,垃圾回收和内存泄漏问题

```

```



33.手写Promise

```

```



35.react相关面试题目
```

``` 