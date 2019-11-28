---
title: ssh远程免密登录
date: 2019-11-19 23:00:24
tags: 
	Linux
	SSH
category:
	Linux 
	shell
---
## 利用ssh key实现Linux免密访问github
使用git bash的windows用户或者linux用户对上传到远端版本库软件（github，gitee等代码托管仓库）时，
发现每次git push 或者是 git pull等命令是需要输入自己的账号和密钥时，
一次两次还好，每次都做这没啥技术含量的动作，就感觉很繁琐和烦躁，
所以，学会使用ssh免密访问必不可少，对我们之后的工作，学习都有好处（这里以linux命令为演示，Windows用git bash一样的处理）

### 1 生成ssh key，使用默认保存位置（注意要求输入密码时直接回车，否则每次要输密码）
	[root@localhost ~]# ssh-keygen -t rsa
	Generating public/private rsa key pair.
	Enter file in which to save the key (/root/.ssh/id_rsa): 
	Enter passphrase (empty for no passphrase): 
	Enter same passphrase again: 
	Your identification has been saved in /root/.ssh/id_rsa.
	Your public key has been saved in /root/.ssh/id_rsa.pub.
	The key fingerprint is:
	SHA256:CvE7bPPDYb1EnQsGsDjs8uqUoiW2XH8g36ycVixmJBw root@localhost.localdomain
	The key's randomart image is:
	+---[RSA 2048]----+
	|      ..         |
	|   E . ..        |
	|  . * .  . . .   |
	|   + =    + o    |
	|  . = o S+ . .   |
	|   = B =o o .    |
	|o.+.* &o o .     |
	|+=o.o+.Bo .      |
	|.+o .=o ..       |
	+----[SHA256]-----+
	[root@localhost ~]#
<!-- more -->
### 2 将公钥文件/root/.ssh/id_rsa.pub上传到github

在个人用户头像选择settings-->>SSH and GPG keys

显示如下

![ssh](https://img-blog.csdn.net/20180609185051636 "ssh")

用命令行输入指令并复制显示出来的数据（或用记事本打开文件，然后拷贝内容到github）

	[root@localhost ~]#cd
	[root@localhost ~]#cd .ssh/
	[root@localhost ~]#cat id_rsa.pub

![key](https://img-blog.csdn.net/20180609185425339 "key")

### 3 测试（切换为ssh方式，而不是默认的http方式）

![test](https://img-blog.csdn.net/20180609190534672 "test")

	[root@localhost github]# git remote add origin git@github.com:username/repository.git
	//username:你的github或其它远程代码托管仓库的用户名，repository:你的克隆仓库
	[root@localhost github]# git push -u origin master