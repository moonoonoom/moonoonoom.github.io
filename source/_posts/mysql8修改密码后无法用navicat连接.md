---
title: mysql8修改密码后无法用navicat连接
date: 2021-06-02 15:44:32
tags: 数据库
categories:
- 编程
- 后端
- 数据库

---

&emsp;&emsp;今天尝试在自己的电脑上用Java连接数据库，但无奈以前设置的root的密码忘记了。尝试去找也没找到（找到了也是加密的我也看不懂）。用navicat可以看一下是几位数，或许可以用来猜一下，不过等我发现的时候已经是我把root密码改了，正要连接navicat的时候。结果连不上，哎，连不上，就是玩。我去搜了一下原来是我的加密格式和navicat需要的不一样。现在我就还原一下我修改的过程。

<!-- more -->

&emsp;&emsp;第一步：以管理员身份运行控制台，关闭mysql服务。

```bash
C:\WINDOWS\system32>net stop mysql
MySQL 服务正在停止.
MySQL 服务已成功停止。
```

&emsp;&emsp;第二步：跳过授权表，进行免密登录。

```bash
system32>mysqld --console --skip-grant-tables --shared-memory
2021-06-02T04:16:21.258780Z 0 [System] [MY-010116] [Server] D:\Study\mysql\mysql-8.0.12-winx64\bin\mysqld.exe (mysqld 8.0.12) starting as process 19392
2021-06-02T04:16:24.043336Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
2021-06-02T04:16:24.197593Z 0 [System] [MY-010931] [Server] D:\Study\mysql\mysql-8.0.12-winx64\bin\mysqld.exe: ready for connections. Version: '8.0.12'  socket: ''  port: 0  MySQL Community Server - GPL.
2021-06-02T04:16:24.264126Z 0 [Warning] [MY-011311] [Server] Plugin mysqlx reported: 'All I/O interfaces are disabled, X Protocol won't be accessible'
```

&emsp;&emsp;第三步：用管理员身份新打开一个cmd，然后登录mysql

```bash
C:\WINDOWS\system32>mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 21
Server version: 8.0.12 MySQL Community Server - GPL

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

&emsp;&emsp;第四步：这时你已经从控制台进入mysql了，接下来你要进行的都是sql操作，在这一步我们就要修改密码了。

&emsp;&emsp;走到这一步就有学问了，因为网上可能给的修改方法是下面这种。

```mysql
update mysql.user set password=password('123456') where user='root';
```

&emsp;&emsp;这种修改方式以及非常之out了，为什么呢，因为这里面有两个字段以及用不了了，就是password和password（），password这个字段以及被废弃了变成了authentication_string，而password（）这个方法mysql8也已经不使用了。

&emsp;&emsp;于是我尝试使用

```mysql
update mysql.user set authentication_string='123456' where user='root';
```

&emsp;&emsp;这样可以成功修改密码，但如果使用

```mysql
select host,user,authentication_string from mysql.user;
```

&emsp;&emsp;查看你修改的密码，你会发现你这一条密码是明文的。这合理吗？这不合理，就算你觉得合理，navicat也觉得不合理，你在navicat输入对应的密码人家根本不认，说密码匹配失败。

&emsp;&emsp;稍微新一点的博文会给出以下这条命令：

```mysql
ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';
```

&emsp;&emsp;但你照这个敲了，你的密码变成密文了，但navicat还是连不上mysql，为什么呢？因为在mysql8.0.以上版本中，caching_sha2_password是默认的身份验证插件，而不是以往的mysql_native_password。但是navicat使用的加密方式依然是mysql_native_password。所以你只好使用这条命令：

```mysql
alter user '用户名'@localhost IDENTIFIED WITH mysql_native_password by '你的密码';
```

&emsp;&emsp;修改成功，皆大欢喜，可以回去继续捯饬java了。

&emsp;&emsp;PS：为什么以前用的时候没遇到这个问题？

