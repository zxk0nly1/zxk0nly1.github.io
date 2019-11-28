---
title: hexoBlog
date: 2019-11-14 20:35:19
tags:
	- hexo
	- JS
categories: Hexo
---
# 工具介绍
---
##  一、安装 nodejs
从[node.js下载页面](https://nodejs.org/en/download/ "nodejs"), 安装一路下一步就ok
![nodejs](https://run-zheng.github.io/2018/09/16/use-hexo-gen-blog-deploy-github/install-nodejs.png "nodejs")
---
## 二、安装hexo
安装完nodejs后， 用npm安装hexo
---
	$ npm install -g hexo-cli 
	$ hexo -v
---
![hexo-v](https://run-zheng.github.io/2018/09/16/use-hexo-gen-blog-deploy-github/install-hexo.png "hexo-v")
---
## 三、使用hexo
---
### 1、用hexo初始化并生成blog
---
	$ hexo init my_hexo
---
![my_hexo](https://run-zheng.github.io/2018/09/16/use-hexo-gen-blog-deploy-github/hexo-init-blog.png "my_hexo")
---
<!-- more -->
### 2、安装依赖，然后用hexo generate，(hexo g)生成静态页面
	$cd my_hexo
	$ls -l
	$npm install
	(这里可能会很慢，所以需要修改一下npm安装源)
	$npm config set registry https://registry.npm.taobao.org 
	（或者下载cnpm）
	$ npm install cnpm -g
	$ cnpm install
	$ hexo generate //生成静态页面
---
![hexo-g](https://run-zheng.github.io/2018/09/16/use-hexo-gen-blog-deploy-github/install-hexo-deps.png "hexo-g")
---
### 3、生成静态页面后，可以用hexo server(或者hexo s)启动服务器，并通过http://localhost:4000访问

![hexo-s](https://run-zheng.github.io/2018/09/16/use-hexo-gen-blog-deploy-github/blog-index.png "hexo-s")

##### 至此，hexo博客就部署好了

*下一讲，可以换一下hexo默认的主题和如何去写一篇博客*

------------



