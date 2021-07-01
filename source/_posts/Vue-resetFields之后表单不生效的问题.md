---
title: Vue resetFields之后表单不生效的问题
date: 2021-07-01 01:33:14
tags: Vue
categories:
- 编程
- 前端
- Vue
---

&emsp;&emsp;最近用ElementUI写一个表单的时候，新增和修改用了同一个表单。那么修改的时候就会有个回填数据，在关闭表单之后需要被清除。我用了`this.$refs.addForm.resetFields();`，然而关闭表单之后，我列表里的对应修改项的这一条数据也被清空了。原来这是因为JS浅拷贝的问题。

<!-- more -->

&emsp;&emsp;我的列表数据是`tableData`，表单数据用的是`addForm`，当我把表单数据赋值给列表项时，用的是：

```javascript
this.$set(this.tableData,this.index,this.addForm);
```

&emsp;&emsp;这就导致了我把`addForm`的地址赋给了`tableData`中对应索引的数据项，那么当我用

```javascript
this.$refs.addForm.resetFields();
```

&emsp;&emsp;清空表单的时候，列表的数据项也被清空了。

&emsp;&emsp;正确的方法是使用解构：

```javascript
this.$set(this.tableData,this.index,{...this.addForm});
```

&emsp;&emsp;问题就解决了。