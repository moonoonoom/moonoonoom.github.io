---
title: 记一次Github Page build failure的经历
date: 2021-05-17 16:18:22
tags: 碎碎念
categories: 编程
---



&emsp;&emsp;昨天想把最近写的博文更新一下。本地运行是成功的，结果`hexo d`之后虽然`deploy done`但是Github一直给我发Page build failure的邮件。我第一反应就是我本地的代码哪里出问题了，但是我只是增加了几个markdown文件，并没有改动其他的地方啊？于是我去网上查了一下，我发现如果github给你发了这个Page build failure的邮件，他一般会在

> The page build failed for the `master` branch with the following error:

 &emsp;&emsp;这句话下面告诉你报错的位置。但是发给我的邮件，这下面只是说了一句

> Unable to build page. Please try again later.

&emsp;&emsp;然后就跟我说有问题可以去看Jekyll文档 ，还有问题的话可以给github发信息问一下。等等，我用的是Jekyll吗，我用的是hexo啊，为什么让我去看Jekyll文档？



&emsp;&emsp; 网上分享的一般都是用Jekyll，极少数的用hexo出现这个问题的，说的是自己的markdown出现语法问题导致编译失败。那为什么我本地能运行成功？然后我看到其中一个网友说，他给github发信息了，github说是因为有一个组件在云端更新了，而他的代码里有部分在组件更新后运行会出bug，而他本地没有更新所以运行没问题。接下来这个网友po了详细的解决过程，非常繁琐。我当时就想，天哪，不会这么倒霉吧，想着我就给github也发了条信息问他怎么回事。结果他回我说

> Hi Luna,
>
> Thanks for writing in, and we apologize for the trouble this is causing.
>
> This sounds like it may be related to an ongoing status event:
>
> [https://www.githubstatus.com](https://www.githubstatus.com/)
>
> Our team is actively working on fixing it. I'd recommend keeping an eye on our status site so you can check when this is resolved. You can also subscribe to that page in order to be notified when the event is over.
>
> Please let us know if you're still having trouble after our status changes back to green. Note that it may take some additional time after that for things to get caught up.
>
> Cheers,
> J.J.

&emsp;&emsp;我说搞咩啊，原来是GitHub那边出问题了，他们说正在修复，我点进这个网页一看，Github Pages对应的那个点还真是黄的。我睡了一觉起来他就修复好了。现在博文可以上传了......

