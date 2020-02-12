---
title: linux服务器远程连接mysql
date: 2019-12-30 19:20:39
tags:
	- linux
	- mysql
categories:
	- 教程
---

#### 1、登录数据库mysql

```shell
[root@Centos ~]# mysql -uroot
mysql> update user set password=password('123456') where user='root' and host='localhost'; 
mysql> flush privileges; 
```

#### 2、设置远程登录

```shell
mysql> GRANT ALL PRIVILEGES ON *.* TO root@"%" IDENTIFIED BY '123456' WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)
mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)
```

![mysql](https://images2018.cnblogs.com/blog/909171/201803/909171-20180325130427485-1646749538.png)

<!--more-->

#### 3、远程Navicat(或者其他mysql管理工具)访问云服务器的数据库

![navicat](https://images2018.cnblogs.com/blog/909171/201803/909171-20180325172145377-665338851.png)

