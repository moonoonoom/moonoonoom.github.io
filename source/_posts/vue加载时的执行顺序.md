---
title: vue加载时的执行顺序
date: 2021-06-16 15:25:27
tags: Vue
categories:
- 编程
- 前端
- Vue
---

&emsp;&emsp;用Vue用了快一年了，很多东西还是一知半解的。之前在公司实习的时候学得不够透彻，只知道改了项目中的文件之后，`npm run serve`就可以运行项目了。等到回到学校自己搭项目，才发现自己其实连Vue项目是从哪里开始加载，怎么加载的都不知道。虽然经常用生命周期的钩子函数，但其实对生命周期也不是很了解。今天这篇博文就来分析一下Vue加载时的执行顺序。



### 1. 项目内文件的执行顺序

&emsp;&emsp;当我们运行`npm run serve`或者`npm run dev`时，项目内的文件运行顺序如下：

> 1. 执行index.html文件
>
> 2. 执行main.js文件
>
> 3. main.js挂载了app.vue文件，用app.vue的templete替换index.html中的
>
>    ```javascript
>    <div id="app"></div>
>    ```
>
>    
>
> 4. main.js中注入了路由文件，将对应的组件渲染到router-view中
>
> 

&emsp;&emsp;这是我在[csdn的一篇博客](https://www.jianshu.com/p/86f6e63f6785)上看的。他后面还有两步“router-view中加载Layout文件”和“Layout 加载Navbar, Sidebar, AppMain”。但我的项目中没有layout文件啊。不知道他啥意思。不过基本的文件执行顺序还是了解了。



### 2. Vue生命周期的执行顺序

&emsp;&emsp;![Vue生命周期状态转换图](https://user-gold-cdn.xitu.io/2020/2/23/170724235e6707f6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

&emsp;&emsp;转化成文字即执行顺序如下:

页面首次加载的执行顺序：

>beforeCreate //在实例初始化之后、创建之前执行
>created //实例创建后执行
>beforeMounted //在挂载开始之前调用
>filters //挂载前加载过滤器
>computed //计算属性
>directives-bind //只调用一次，在指令第一次绑定到元素时调用
>directives-inserted //被绑定元素插入父节点时调用
>activated //keek-alive组件被激活时调用，则在keep-alive包裹的嵌套的子组件中触发
>mounted //挂载完成后调用
>
>大括号大括号//mustache表达式渲染页面

修改data时的执行顺序

>watch //首先先监听到了改变事件
>filters //过滤器没有添加在该input元素上，但是也被调用了
>beforeUpdate //数据更新时调用，发生在虚拟dom打补丁前
>directived-update //指令所在的组件的vNode更新时调用，但可能发生在其子vNode更新前
>directives-componentUpdated//指令所在的组件的vNode及其子组件的vNode全部更新后调用
>updated //组件dom已经更新

组件销毁时的执行顺序

>beforeDestroy //实例销毁之前调用
>directives-unbind //指令与元素解绑时调用，只调用一次
>deactivated //keep-alive组件停用时调用
>destroyed //实例销毁之后调用

### 3. Vue组件内方法的执行顺序

&emsp;&emsp;那么vue组件内的方法的执行顺序是怎样的呢？由Vue的[源码](https://github.com/vuejs/vue/blob/dev/src/core/instance/state.js#L45-L53)

```javascript
export function initState (vm: Component) {
  vm._watchers = []
  const opts = vm.$options
  if (opts.props) initProps(vm, opts.props)
  if (opts.methods) initMethods(vm, opts.methods)
  if (opts.data) {
    initData(vm)
  } else {
    observe(vm._data = {}, true /* asRootData */)
  }
  if (opts.computed) initComputed(vm, opts.computed)
  if (opts.watch && opts.watch !== nativeWatch) {
    initWatch(vm, opts.watch)
  }
}
```

&emsp;&emsp;可知，方法的执行顺序为prop、methods、data、computed、watch。

&emsp;&emsp;为啥是先执行methods再执行data？如果methods中用到data的数据怎么办？

&emsp;&emsp;可惜，再往下的源码我看不懂，等我变强再说吧。