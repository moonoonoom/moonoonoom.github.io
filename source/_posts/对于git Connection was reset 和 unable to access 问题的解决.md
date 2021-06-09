---
title: 对于git Connection was reset 和 unable to access 问题的解决
date: 2021-06-09 19:19:26
tags: git
categories: 编程
---

&emsp;&emsp; 使用git拉取代码的时候经常报错，错误信息如下：

```bash
OpenSSL SSL_connect: Connection was reset in connection to github.com:443
```

&emsp;&emsp;我知道一般报这个错是网络问题，但没道理一直网络问题吧，实验室其他人怎么没网络问题呢。拉了几十次都有了还是这样。去网上查了一下才知道可能是代理问题，是我用了我VPN的关系。

&emsp;&emsp;解决方法是执行这条命令：

```bash
git config --global --add remote.origin.proxy "127.0.0.1:1080"
```

&emsp;&emsp;其中”1080“部分应该是代理的https端口号。

&emsp;&emsp;同样地，对于git 报错

```bash
fatal: unable to access 'https://github.com/...'
```

&emsp;&emsp;应该设置

```
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
```

&emsp;&emsp;其中”1080“部分也应该是代理的https端口号。