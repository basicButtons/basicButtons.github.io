---
layout: post
title: Event Loop
date: 2021-08-08
tags: note
---

<h2 align="center">Event loop</h2>

一、宏任务和微任务

Macro-task（宏任务）

1. 主线程代码（script中的代码）
2. setTimeout
3. setInterval
4. requestAnimationFrame
5. I/O流
6. UI render（页面UI渲染）
7. ajax请求

微任务

micro-task

1. process.nextTick
2. Promise.then方法
3. Async/await（实际上还是Promise）
4. Mutation Observer（h5的新特性）
5. onclick触发的函数
