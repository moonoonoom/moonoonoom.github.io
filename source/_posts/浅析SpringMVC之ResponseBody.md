---
title: 浅析SpringMVC之ResponseBody
date: 2021-05-22 18:55:15
tags: SpringMVC
categories:
- 编程
- 后端
- Java
- SpringMVC
---

&emsp;&emsp;最近刚刚开始做SpringBoot的项目，用的前后端分离，由于时间问题部分代码是照着网上的写的，没有理解代码的意义，导致我闹了个乌龙。我在后端写响应get请求的方法时，没有加`@ResponseBody`的注解，于是我前端发出get请求之后一直返回404。我还觉得很奇怪，明明我请求的地址是没问题的。甚至还去StackOverflow上问了一下，搞了快一个晚上。

<!-- more -->

&emsp;&emsp;那么这个`@ResponseBody`究竟是干什么的呢？`@ResponseBody`注解的作用是将controller的方法返回的对象通过适当的转换器转换为指定的格式之后，写入到response对象的body区，通常用来放回JSON数据或者XML数据。使用此注解之后不会再走视图处理器，而是直接将数据写入到输入流中，效果等同于通过response对象输出指定格式的数据。

&emsp;&emsp;为什么不加`@RespnseBody`就会返回404呢。我推测是因为不加这个注释，系统默认这个方法返回的是视图，因此我前端（这里用的vue）请求不到对应的方法，所以返回状态码404。为什么前端请求不到对应的方法？这里我推测是ajax请求会把返回值类型加到方法名里进行匹配。这一段的猜测都等到日后有时间了再证实。

&emsp;&emsp;顺道一提，在controller类前面加`@RestController`注解相当于给类里的每个方法前面加了`@ResponseBody`，同样地，这个类里面的方法也不能返回视图了。