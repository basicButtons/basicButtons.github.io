---
layout: post
title: JAVA第二章
date: 2019-11-15
tags: JAVA
---

## 第二章 基本数据类型和操作 

#### 常数 

```java
final double PI = 3.14159; 
```



#### 基本数据类型 - 数值型 

```java
System.out.println("Byte's size : 8bits");//specially Byte don't have the method Size!!!
        System.out.println("Short's size: " + Short.SIZE);
        System.out.println("int's size : " + Int.SIZE);
        System.out.println("long's size : "+ Long.SIZE);
        System.out.println("float's size:" + Float.SIZE);
        System.out.println("double's size : "+Double.SIZE);
```

![res1](/Users/maxuan/Desktop/basicButtons.github.io/images/java/res1.png)



#### 数值类型转换：

1. 不能对boolean类型进行类型转换。
2. 不能把对象类型转换成不相关类的对象。
3. 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。
4. 转换过程中可能导致溢出或损失精度。
5.  浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入

##### 自动类型转换

- 必须满足转换前的数据类型的位数要低于转换后的数据类型
- ![typeChange](/Users/maxuan/Desktop/basicButtons.github.io/images/java/typeChange.jpg)

##### 强制类型转换

- 在value前面加上（datatype）



#### 运算符

布尔运算符又称为逻辑运算符，对布尔值 进行运算，结果也是布尔值 

&& 条件与 （当第一个条件为false，不再进行第二个计算）

||  条件或（当第一个条件为ture，不再进行第二个计算）

&    无条件与

|    无条件或

!     非

^    异或





 