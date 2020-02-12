---
title: win系统安装nodejs配置
date: 2019-12-12 20:27:07
tags:
	- Node
categories:
	- 教程
---

# Node配置

1. #### 安装node

   Node.js 安装包及源码下载地址为：<https://nodejs.org/en/download/>。 

   ![nodejs](https://www.runoob.com/wp-content/uploads/2014/03/download-page.jpg)

   **另外，如果没有设置全局目录node_global，那么全局安装的文件将会保存到 C:\Users\computer\AppData\Roaming\npm (computer是自己设置的计算机名字)** 

<!--more-->

2. #### 配置node_global和node_cache

   (1). 在node安装目录创建node_global和node_cache文件夹

    ![node_global](https://img-blog.csdn.net/2018102321082540?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Njb3JwaW9fbWVuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   #### (2) . 

   ##### 用户变量设置：将用户变量中 PATH 的值改成 D:\Program Files\nodejs\node_global，没有PATH，可以直接添加。

   ##### 系统变量设置：添加变量 NODE_PATH  值为：D:\Program Files\nodejs\node_modules

   ![node_path](https://img-blog.csdn.net/20181023211854153?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Njb3JwaW9fbWVuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

   #### (3). 打开cmd

   **npm config set prefix "D:\Program Files\nodejs\node_global"**   

   **npm config set cache "D:\Program Files\nodejs\node_cache"**

   ![cmd](https://img-blog.csdn.net/20181023211035231?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Njb3JwaW9fbWVuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

3. #### 使用npm安装模块

**执行npm install express -g 后，查看node_global 文件夹** 

![express](https://img-blog.csdn.net/20181023212141580?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3Njb3JwaW9fbWVuZw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

*有时候用npm拉取包可能会很慢*  **可以用淘宝npm镜像代替npm进行拉包** 

##### 执行：

```shell
$ npm install -g cnpm --registry=https://registry.npm.taobao.org 
```

**然后就可以用 <u>cnpm install express -g</u> 进行拉包了，和npm一样。** 





