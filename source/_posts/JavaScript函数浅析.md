---
title: JavaScript函数浅析
date: 2021-08-24 20:22:54
tags: JS
categories:
- 编程
- 前端
- JavaScript
---

&emsp;&emsp;函数是Function类型的实例，所以函数是对象。函数名是指向函数对象的指针，并且不一定与函数本身紧密绑定。ES6新增了使用胖箭头`=>`语法定义函数表达式的能力，很大程度上箭头函数实例化的函数对象与正式的函数表达式创建的函数对象行为是相同的，任何可以使用函数表达式的地方都可以使用箭头函数（但是箭头函数和普通函数还是不同的哦~）。

<!-- more -->

### 1.箭头函数

&emsp;&emsp;箭头函数的语法是：

```javascript
(a,b) => {
    return a + b;
}
```

&emsp;&emsp;等同于：

```javascript
function(a,b){
    return a + b;
}
```

&emsp;&emsp;如果只有一个参数也可以不用写括号：

```javascript
x =>{
    return 2 * x;
}
```

&emsp;&emsp;没有参数或者多个参数的情况下则必须写括号：

```javascript
() =>{
    return 1;
}
```

&emsp;&emsp;箭头函数也可以不写大括号，但这样会影响函数的行为。使用大括号就说明包含“函数体”，没有大括号，那么箭头函数后面只能由一行代码，并且会隐式返回这行代码的值。

&emsp;&emsp;箭头函数不能使用arguments、super和new.target，也不能用作构造函数，同时没有prototype属性。
