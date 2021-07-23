---
title: vue学习笔记：Unexpected mutation of prop
date: 2021-07-23 21:44:16
tags: Vue
categories:
- 编程
- 前端
- Vue
---

&emsp;&emsp;今天在工作的时候遇到了vue的这个bug。原来是因为Vue的Prop是单向数据流，父组件的更新会流动到子组件的prop中，但是子组件不可以自己改变prop的值。

<!-- more -->

&emsp;&emsp;看看报错那一行，我是直接复制的AntD官方文档的代码：

```html
<a-modal v-model:visible="visible" title="Basic Modal" @ok="handleOk">
```

&emsp;&emsp;而visibile就是props中报错的那个变量。

&emsp;&emsp;但是我感觉没有改visible中的值呀？问了下前辈才知道原来v-model提供的是双向绑定！上面这样写可能表达不清楚，我们这样写：

```html
v-model:a="b"
```

&emsp;&emsp;这样如果a改变了b的值也会改变，如果b改变了a的值也会给改变。所以Vue才报错了，因为我给了a在组件内修改b的权限，而b作为props中的属性是不应该在子组件中被修改的。

&emsp;&emsp;这也是v-model和v-bind的区别，v-model是双向绑定，v-bind是单向绑定。
