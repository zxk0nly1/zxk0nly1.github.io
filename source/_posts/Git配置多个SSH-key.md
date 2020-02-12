---
title: Git配置多个SSH-key
date: 2019-12-15 00:48:30
tags:
	- Git
categories:
	- 教程
---

# GIT配置多个ssh公钥

## 1 背景

##### 当有多个git账号时，比如： 

a. 一个**gitee**，用于公司内部的工作开发；

 b. 一个**github**，用于自己进行一些开发活动； 

## 2 解决方法

1. ##### 生成一个公司用的SSH-Key 

   ```shell
   $ ssh-keygen -t rsa -C 'xxxxx@company.com' -f ~/.ssh/gitee_id_rsa生成一个github用的SSH-Key 
   ```

2. ##### 生成一个github用的SSH-Key 

   ```shell
   $ ssh-keygen -t rsa -C 'xxxxx@qq.com' -f ~/.ssh/github_id_rsa
   ```

<!--more-->

3.  ##### 在 ~/.ssh 目录下新建一个config文件，添加如下内容（其中Host和HostName填写git服务器的域名，IdentityFile指定私钥的路径） 

   ```shell
   # gitee
   Host gitee.com
   HostName gitee.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/gitee_id_rsa
   # github
   Host github.com
   HostName github.com
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/github_id_rsa
   ```

4. ##### 用ssh命令分别测试 

      ```shell
      $ ssh -T git@gitee.com
      $ ssh -T git@github.com
      ```

      这里以***gitee***为例，成功的话会返回下图内容 

      ![gitee](https://images.gitee.com/uploads/images/2018/0921/161137_b71ef6be_967230.png)