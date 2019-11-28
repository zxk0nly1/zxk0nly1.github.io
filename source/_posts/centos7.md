---
title: centos7
date: 2019-11-14 19:02:29
tags:
	- linux
	- LAMP
toc: true
categories: OS
---
# centos7搭建LAMP环境
---
## yum安装
---
### 1.安装apache
---
#### 实验环境：
	$ sudo cat /etc/redhat-release
---
#### 安装apache
	$ sudo yum -y install httpd httpd-devel
---
#### 启动apache服务
	$ sudo systemctl httpd start
---
#### 设置httpd服务开机启动
	$ sudo systemctl enable httpd
---
#### 查看服务状态
	$ sudo systemctl status httpd
---
#### 防火墙设置开启80端口
	$ sudo firewall-cmd --permanent --zone=public  --add-service=http
	$ sudo firewall-cmd --permanent --zone=public  --add-service=https
	$ sudo firewall-cmd --reload	
---
#### 确认80端口监听中
	$ ss -tulp | grep httpd
---
#### 查服务器IP
	$ ip addr
---
<!-- more -->
#### 浏览器登陆
---
![img](https://images2015.cnblogs.com/blog/1054216/201707/1054216-20170721173607855-676796079.jpg)
apache环境搭建成功！
---
### 2.安装mysql
---
#### 安装mysql
	$ sudo yum install mariadb mariadb-server mariadb-libs mariadb-devel
	$ sudo rpm -qa | grep mariadb
---
#### 开启mysql服务，并设置开机启动，检查mysql状态
	$ sudo systemctl start  mariadb
	$ sudo systemctl enable  mariadb 
	$ ss -tulp |grep mysqld
---
#### 数据库安全设置
	$ sudo mysql_secure_installation (yynyyy)
---
#### 登陆数据库测试
	$ mysql -uroot -p(输入设置好的密码)
	MariaDB [(none)]> show databases;
---
### 3.安装php
---
#### 安装php
	$ sudo yum -y install php
	$ sudo rpm -ql php
---
#### 连接mysql与php
	$ sudo yum -y install php-mysql
	$ sudo rpm -ql php-mysql
---
#### 安装php常用模块
	$ sudo yum install -y php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel php-bcmath
---
#### 测试php
	$ cd /var/www/html
	$ ls
	$ pwd
	$ vi info.php

<?php
phpinfo();
?>



(按esc退出输入，输入':wq',保存并退出)
---
#### 重启apache服务器
	$ sudo systemctl restart http
---
#### 测试PHP
	在自己电脑浏览器输入服务器的ip/info.php(如192.168.190.130/info.php)，你可以看到已经安装的模块；
![img](https://images2015.cnblogs.com/blog/1054216/201707/1054216-20170725104919468-1062733523.jpg)

##### 至此，你的centos7的Apache+Mysql+Php环境就搭建好了