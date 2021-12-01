---
layout: post
title: network-HTTP-content-type
date: 2021-07-29
tags: network
---

<h2 align="center">content-type</h2>
在`koa-bodyparser`中有针对不同的`Content-Type`来返回body。
json 数据  application/json、application/json-patch+json、application/vnd.api+json  使用RESTful json API接口设计
form 表单  application/x-www-form-urlencoded   常见的表单交互方式
text 文本  text/plains 

multipart/form-data
由于这种方式将数据有很多部分,它既可以上传键值对,也可以上传文件,甚至多个文件。当上传的字段是文件时,会有Content-Type来说明文件类型;Content-disposition,用来说明字段的一些信息。每部分都是以-boundary开始,紧接着是内容描述信息,然后是回车,最后是字段具体内容(字段、文本或二进制等)。如果传输的是文件,还要包含文件名和文件类型信息。消息主体最后以-boundary-标示结束。
// 这个地方需要后面写一个东西去验证。



Hpack 是在字节三面中提到的一个问题，就是说为什么 cookie 不能用来存储数据呢？
cookie太大，会导致头部太大。HTTP头是比较长的，如果发送的数据比较小时，也得发送一个很大的HTTP头部。
有的时候对于一个HTTP报文而言，它的头部占据整个报文的90%以上，会导致网络的吞吐率不高。并且，比较大的HTTP头部会迅速占满慢启动过程中的拥塞窗口，导致延迟加大。所以引入了一些进行方式对头部进行压缩。