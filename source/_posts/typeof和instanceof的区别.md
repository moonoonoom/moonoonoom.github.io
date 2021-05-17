---
title: typeof和instanceof的区别
date: 2021-05-15 21:46:13
tags: JavaScript
categories:
- 编程
- 前端
- JavaScript
---



&emsp;&emsp;`typeof`用来判断一个变量是否为原始类型，即是否为6种原始值：Null, Undefined, Boolean, Number, String, Symobl 中的一种。其用法为

```javascript
let a = "";
console.log(typeof a);//string
```



&emsp;&emsp;使用`typeof`判断变量，将会返回变量对应的类型。如果该变量是引用值，那么不管它是什么对象，`typeof`都会返回`object`。值得注意的是，如果该变量是原始值中的Null类型，`typeof`也会返回`object`。



&emsp;&emsp;`typeof`只能判断一个变量是什么原始类型，对于引用类型，它只能返回`object`，与之相对`instanceof`就是用来判断一个变量是不是给定引用类型的。其用法为

```javascript
result = variable instanceof constructor
```

​		原型链决定了一个变量是不是给定引用类型。因为所有引用值都是`Object`的实例，所以通过`instanceof`检测任何引用值和`Object`构造函数都会返回`true`。同样的，如果用`instanceof`检测原始值，则始终会返回`false`，因为原始值不是对象。



&emsp;&emsp; 因此，`typeof`和`instanceof`的区别有两个：

&emsp;&emsp;1. 用法不一样，`typeof`返回待判断变量的类型，`instanceof`则相当于==，判断该变量是否为我给出的类型。

&emsp;&emsp;2. 判断的值类型不一样，`typeof`用来判断原始值，`instanceof`用来判断引用值。

