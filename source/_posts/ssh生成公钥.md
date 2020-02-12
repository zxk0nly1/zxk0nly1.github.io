---
title: ssh生成公钥
date: 2019-12-15 00:37:29
tags:
	- ssh
categories:
	- 教程
---

## SSH公钥

##### gitee和github等版本库软件，提供了基于ssh协议的Git服务，在使用ssh协议访问仓库之前，需要先配置好账户/仓库的SSH公钥。 

### 你可以按如下命令来生成 sshkey: 

```shell
ssh-keygen -t rsa -C "xxxxx@xxxxx.com"  
# Generating public/private rsa key pair...
```
<!--more-->
##### 按照提示完成三次回车，即可生成 ssh key。通过查看 `~/.ssh/id_rsa.pub` 文件内容，获取到你的 public key  

```shell
cat ~/.ssh/id_rsa.pub
# ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC6eNtGpNGwstc....
```

![ssh](https://images.gitee.com/uploads/images/2018/0814/170141_5aa5bc98_551147.png)

##### 复制生成后的 ssh key，通过仓库主页 **「*管理」->「部署公钥管理」->「添加部署公钥」*** ，添加生成的 public key 添加到仓库中。

![id_rsa.pub](https://images.gitee.com/uploads/images/2018/0814/233212_29a62378_551147.png)

添加后，在**终端（Terminal）**中输入  :

```shell
ssh -T git@gitee.com
```

首次使用需要确认并添加主机到本机SSH可信列表。若返回 

```shell
Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access.
```

内容，则证明添加**成功**。

![gitee](https://images.gitee.com/uploads/images/2018/0814/170837_4c5ef029_551147.png)

**添加成功后，就可以使用SSH协议对仓库进行操作了。**  

