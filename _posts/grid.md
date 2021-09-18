---
layout: post
title: grid布局
date: 2021-08-11
tags: note
---

<h2 align = "center">Grid 布局</h2>

### 一、容器属性

#### 1.1 display:grid

对于容器而言要想使用grid布局，首先要像flex布局一样在容器层面声明`display:flex` 

```css
.container{
	display:grid
}
```



#### 1.2 grid-template-columns 属性， grid-template-rows 属性

对于容器而言：要对行和列进行划分：grid-template-columns 是对列进行划分、grid-template-rows是对行进行划分，确定每一个列行的宽度和高度。

```css
.container{
	grid-template-columns:100px 100px 100px;
	grid-template-rows:100px 100px 100px;
}
// 以上是使用绝对定位，但是同时可以使用相对定位来进行描述
.container{
  grid-template-rows:33% 33% 33%;
  grid-template-columns:33% 33% 33%;
}
```

##### (1) repeat

有的时候我们觉得重复的属性，我们不想去写，就可以去使用repeat减少麻烦。比如上面的代码就可以利用repeat进行简写。

```css
.container{
	grid-template-rows:repeat(3,33%)
	grid-template-columns:repeat(3,33%)
}
```

`repeat` 函数的第一个函数是重复的次数，第二个参数重复的对象。而且重复一个模式也是可以的。

```
.container{
	grid-template-rows:repeat(3,"100px 200px 50px");
}
```

#### (2)auto-fill 关键词

有时候元素的大小是固定的，这样的话，我们就可以使用 `auto-fill` 关键词，来进行减少重复。

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

![image-20210811222332690](/Users/maxuan/Library/Application Support/typora-user-images/image-20210811222332690.png)

