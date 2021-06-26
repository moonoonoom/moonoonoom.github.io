---
title: JavaScript构造函数模式
date: 2021-06-26 16:15:10
tags: JS
categories:
- 编程
- 前端
- JavaScript
---

&emsp;&emsp;JavaScript中的构造函数的特点是：没有显示地创建对象、属性和方法直接赋值给了this、没有return。

<!-- more -->

&emsp;&emsp;当我们用new创建构造函数时，会执行如下操作：

1. 在内存中创建一个新对象。
2. 把新对象内部的Prototype的特性赋值为构造函数的Prototype属性。
3. 构造函数内部的this指向这个新对象。
4. 执行构造函数内部的代码（给新对象添加属性）。
5. 如果构造函数的返回类型是非空对象，则返回该对象；否则返回刚创建的新对象。

&emsp;&emsp;第五句啥意思？

&emsp;&emsp;让我们来看看源码：

```javascript
function objectFactory() {
  let newObject = null;
  let constructor = Array.prototype.shift.call(arguments);
  let result = null;
  // 判断参数是否是一个函数
  if (typeof constructor !== "function") {
    console.error("type error");
    return;
  }
  // 新建一个空对象，对象的原型为构造函数的 prototype 对象
  newObject = Object.create(constructor.prototype);
  // 将 this 指向新建对象，并执行函数
  result = constructor.apply(newObject, arguments);
  // 判断返回对象
  let flag = result && (typeof result === "object" || typeof result === "function");
  // 判断返回结果
  return flag ? result : newObject;
}
// 使用方法
objectFactory(构造函数, 初始化参数);
```

&emsp;&emsp;即如果return的是object或function，则return这个结果，反正就return创建的新对象（this）。

&emsp;&emsp;构造函数也是函数，构造函数和普通函数的唯一区别就是调用方式不同。任何函数只要用new调用就是构造函数。而构造函数不使用new调用也是普通函数。那么这时候构造函数内部的this指向谁呢？值得注意的是：**再调用一个函数而没有明确设置this值的情况下（即没有作为对象的方法调用，或者没有使用call()/apply()调用），this始终指向gobal对象（在浏览器中就是window对象）。**

&emsp;&emsp;鉴于函数也是一种对象。如果在构造函数内部定义了函数，那么每一次构造对象的时候都会创建一个明明作用一样，但是是不同对象的方法。比较好的办法是把这个方法写在构造函数外面，再赋值进构造函数里面，比如

```javascript
function Person(){
    this.sayName = sayName;
}
function sayName(){
    console.log(this.name);
}
```

&emsp;&emsp;这样Person()里的sayName就只是一个指向外部的指针。