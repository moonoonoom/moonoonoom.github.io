---
title: bug记录与解决方法 part1
date: 2021-08-17 23:25:08
tags: bug
categories:
- 编程
- 前端
- bug
---

&emsp;&emsp;流水账式地记录bug，再小的bug都有学习的价值！

<!-- more -->

### 1. 行内元素修改样式不生效

&emsp;&emsp;行内元素不能修改宽高，要改成inline-block。inline-block中的content会像block一样上下自动居中，解决方法见：行内元素对不齐的三种解决方法。默认的行高一般是根据字号。

### 2. vue3-父子元素传值时父元素值的更改没有响应到子元素

&emsp;&emsp;这篇可以单独写一篇文章，暂且按下不表。

### 3. 在表格内点击一次按钮弹窗会弹两次

&emsp;&emsp;弹窗弹两次说明渲染了两次，这时候就要去html代码里找为什么会渲染两次。在html代码里没有显式地渲染两次，但观察发现我把弹窗的代码写进表格的代码内了。表格自然是有几行数据就渲染几次，正好这里有两份数据，所以使弹窗也渲染了两次，应该把弹窗写在外面。

### 4. Prop传值

&emsp;&emsp;其实我prop传值一直没搞太懂，今天遇到问题才知道，父组件里面

```html
:a="b"
```

&emsp;&emsp;这里的a对应的是子组件里：

```java
props:['a']
```

&emsp;是这里的a啊，只要这两个对上了就可以传值了。

### 5. 对弹框内元素应用父子选择器不生效

&emsp;&emsp;首先我们公司用的是less，语法上和css会有一点区别。

&emsp;&emsp;这不是重点，重点是父子选择器为啥不生效呢？

&emsp;&emsp;我的文件结构是：

```html
<template>
  <div class="box">
    <a-modal 
      :afterClose="afterClose" 
      v-model:visible="modalVisible" 
      v-model:title="modalTitle"
      @ok="handleOk"
      width="1000px"
      :footer="null"
    >
      <a-table
        v-model:data-source="tableData"
        :columns="columns"
        :showHeader="false"
        :pagination="false"
      > 
          <template #version="props">
            <span class="version">
              v{{ props.record.version.toFixed(1) }}
            </span>     
        </template>
```

&emsp;&emsp;而我的less写的是：

```less
.box{
  .version{
    background-color:#178CF7 ;
    color:white;
    padding: 0 5px 0 3px;
    border-radius: 10%;
    margin-left:4px;
    cursor: pointer;
  }
}
```

&emsp;&emsp;看起来没问题，但其实对话框Modal在渲染的时候是挂在body上的，而不是挂在其父divbox上的，所以box并不是version的祖先。为什么要这么设计？因为如果把对话框挂载在box上，box又挂载在调用它的组件上，那么其实boxhui被挤到画面外。只有把对话框挂载在body上，才能比较方便地显示在画面中间。

&emsp;&emsp;antd的对话框有一个”wrapClassName“属性，代表对话框外层容器的类名，把它设置为我们想要的名字，就能应用父子选择器啦。

### 5. v-if判断结果和预期结果不一致

&emsp;&emsp;v-if里面如果要判断方法需要在方法后面加上括号，不然就变成判断变量了。

### 6. Failed to resolve component: Header

&emsp;&emsp;Header这个组件引入之后放在components里面声明，不是setup的return！

 ###   7. div设置height:100%;无效

### 8. vue获取变量的变量名

### 9. 一个组件渲染了一百多遍

&emsp;&emsp;修改ref会造成组件重新渲染，但我又把修改的方法写在组件的html里了，导致死循环。那为什么是循环一百多遍呢，是vue内部有个防止死循环的机制，循环一百遍以上就跳出了。

### 10. div一个高度固定，另一个高度自适应

&emsp;&emsp;用flex布局，高度固定的那个写高度，另一个flex: 1。但是这样做之后flex：1的这个div会被子元素撑开。

&emsp;&emsp;推荐用calc（100vh-?px）。
