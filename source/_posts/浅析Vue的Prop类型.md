---
title: 浅析Vue的Prop类型
date: 2021-05-16 21:08:52
tags: Vue
categories:
- 编程
- 前端
- Vue
---



&emsp;&emsp;Prop是Vue的组件用来进行通讯的一个attribute，被用来向子组件传递数据。HTML中的attribute名是不区分大小写的，因此使用DOM模板时，用驼峰命名法的prop名需要使用等价的短横线分割命名法来命名。但是如果使用的是字符串模板，这个限制就不存在了。



&emsp;&emsp;Prop的定义方式可以是

```javascript
props: ['title', 'likes', 'isPublished', 'commentIds', 'author']
```

&emsp;&emsp;也可以是

```javascript
props: {
  title: String,
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

&emsp;&emsp;其中第二种方式给每个prop都指定了值的类型。

&emsp;&emsp;也可以在定义prop的时候给它一个默认值，其方法是

```javascript
props: {
      a: {
        type: Boolean,
        default: true
      }
    }
```

&emsp;&emsp;在同一个组件中，data定义的变量和prop定义的变量不能同名，否则会报错。如果这个变量要用来在组件之间通信，那么就不要定义成data，应该定义成prop。

