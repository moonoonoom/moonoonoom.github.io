---
title: vue3使用AntD图标不生效/vue报错emptyicon
date: 2021-07-23 21:37:29
tags: Vue
categories:
- 编程
- 前端
- Vue
---

&emsp;&emsp;vue3使用AntD的图标应该用其2.x版本而非1.x版本，然而AntD文档页面进去默认是1.x版本。那么就会不生效，并且报错`empty icon`。那么2.x版本应该怎么用呢？

<!-- more -->

&emsp;&emsp;首先是1.x版本的用法：

```html
<a-icon type="step-backward" />
```



&emsp;&emsp;没啥好说的，直接用就完事了。

&emsp;&emsp;2.x版本复制出的代码是这样的（右上角改版本）：

```html
<StepBackwardOutlined />
```

&emsp;&emsp;那光用就不行了，还得引入。

&emsp;&emsp;首先import：

```javascript
import {
  StepBackwardOutlined
} from "@ant-design/icons-vue";
```

&emsp;&emsp;其次把它放到components中：

```javascript
 components: {
   StepBackwardOutlined
  }
```

&emsp;&emsp;就可以用啦~
