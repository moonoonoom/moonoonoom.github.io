---
title: vue3学习笔记：Setup
date: 2021-07-22 23:41:33
tags: Vue
categories:
- 编程
- 前端
- Vue
---

&emsp;&emsp;不用不知道，原来vue3和vue2差别还是蛮大的。在学习过程中第一个接触到的就是，vue3中数据不推荐写在data()中（当然你想写也可以写，v3对v2是兼容的），而是写在setup()里，那么setup是什么？

<!-- more -->

&emsp;&emsp;setup的设计是为了组合式api（组合式api是什么？以后再写吧...）。vue3使用setup是为了把data、computed、methods、watch中的内容抽离在一个函数里，提高组件内代码的可阅读性。就像data()一样，setup()必须return一个对象。

&emsp;&emsp;setup在生命周期中位于created和beforeCreated之前，所以它被用于代替created和beforeCreated。在setup函数里不能访问到this。

&emsp;&emsp;setup里面创建的变量不是响应式的，因此可以使用ref来创建响应式的变量。

&emsp;&emsp;（待续）
