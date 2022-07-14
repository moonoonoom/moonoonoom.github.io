---
title: 使用github+hexo+Volantis搭建博客时踩过的坑
date: 2021-03-05 23:32:11
tags:
- git
- hexo
categories:
- 编程
- 前端
- 博客
---





&emsp;&emsp;第一个帖子记录一下我搭博客遇到的奇葩问题，均已解决。都是比较小白的问题。

<!-- more -->

###  **1. 安装hexo报错**



&emsp;&emsp;一开始安装node.js时就踩坑了，当时参考的教程直接给了个链接我就图省事点进去下了，结果这个版本不是最新的，导致我之后用git安装Hexo的时候一直报错。



报错信息如下：

```bash
console.js:39
	throw new ERR_CONSOLE_WRITABLE_STREAM('stdout');
	^
```

这是Node的官方下载地址：[Node下载网址](https://nodejs.org/zh-cn/)



### **2. chrome不能访问google和github**

&emsp;&emsp;搞到一半的时候，chrome突然不能访问google和github了，用edge还是可以正常访问。进入**chrome://settings/ 高级-系统** 发现在“打开您的计算机的代理设置”下面显示我的chrome被第三方插件接管了。把这个点掉之后就又能访问了。不过如果我的chrome一早被接管了，为什么突然不能访问？难道我的chrome突然被接管了？这里没弄懂。





### **3. 本地同步到网络出问题**

&emsp;&emsp;如果要将本地网页同步到云端，应该使用hexo d。如果还要备份本地文件，应该在git上新建一个分支进行同步。这样两个分支一个用来放hexo部署的信息，一个用来同步本地的文件。但我当时同步的时候把git的操作和hexo的操作弄混了，导致把本地的文件上传到了git与网页相关联的分支上。这样我每次push之后我的_config.yml文件都会报错，疯狂给我的邮箱发信息，原来可以访问的网页也变成404了。





### **4. 修改_config.yml文件不生效**

&emsp;&emsp;修改_config.yml文件中的属性时，属性名和内容之间必须有空格如jinrishici: false，不然识别不出来。





### **5. 博客最下面的访问量和访问人数显示不正确**

&emsp;&emsp;一开始一直是上万的访问量和人数，一看就不是我的。原来是我最开始hexo的_config.yml里的网址忘记改成自己的网址了。就好像抄作业把别人的作业也抄上去了一样，盲抄作业害死人呐。





### **6. Volantis如何自动生成文章目录**

&emsp;&emsp;需要三级标题，不过没看到哪里有说啊？



### **7. Markdown中文段落首行缩进**

&emsp;&emsp;Markdown虽然很好用，但是对于中文的首行缩进不太友好。这里选择用`全方大的空白&emsp;`进行强制缩进。（虽然有点麻烦）