---
title: CSS的动画效果
date: 2021-06-17 09:57:24
tags: CSS
categories:
- 编程
- 前端
- CSS
---

&emsp;&emsp;CSS的动画分为两种类型：transition和animation。其中transition又称”过渡“，需要由事件触发，并且只有一组关键帧（开始-结束）。animation不需要由时间触发不说，且可以设置多组关键帧。

<!-- more -->

### 1. Transition

&emsp;&emsp;transition有四个属性：

>**transition-property**
>
>执行过渡的属性，例子设置为颜色color的变化，也可以是width, font-size等，不设置的话默认是all，即所有属性；
>
>**transition-duration**
>
>过渡的时间，单位是秒，如1s, 2.3s，不设置的话默认 0s，即无过渡效果；
>
>**transition-timing-function**
>
>设置过渡时的变化方式，默认是 ease，即速度由慢到快再到慢，常用的还有 linear，线性变化速度均匀，还有其他几个方式，过渡时间短的话看不出什么区别；
>
>**transition-delay**
>
>延迟时间，即多少秒后执行过渡效果，默认 0s，不延迟

&emsp;&emsp;transition可以写成:

```css
transition-property: color;
transition-duration: 2s;
transition-timing-function: linear;
transition-delay: 0;
```

&emsp;&emsp;但这么写太繁琐了，实际应用的时候一般写成：

```css
transition: color 2s linear;
```



### 2. Animation

&emsp;&emsp;animation需要和@keyframes属性配合使用。@keyframes也是写在style中，其写法为

```css
@keyframes a {
  0% { background: #c00; }
  50% { background: orange; }
  100% { background: yellowgreen; }
}
```



&emsp;&emsp;keyframe顾名思义就是关键帧，那么keyframes就是很多个关键帧的结合。在上面这段代码中，大括号内的三个百分比分别代表动画的三个状态。可以把动画想象成进度条，那么这三个百分比就是进度条中的三个节点。如果有需要还可以加入更多节点。其中0%可以用from代替，100%可以用to代替。

### 3. Transform

&emsp;&emsp;css还有个transform属性，需要与animation配合使用。transform代表变形的意思。如果想让div旋转、位移、变形、放大缩小，那么都需要用到transform。其用法为：

```css
transform: rotate(10deg);
```

&emsp;&emsp;其属性有：

>旋转rotate（中心为原点）
>扭曲、倾斜skew（skew(x,y), skewX(x), skewY(y)）
>缩放scale（scale(x,y), scaleX(x), scaleY(y)）
>移动translate（translateX,translateY）
>矩阵变形matrix

