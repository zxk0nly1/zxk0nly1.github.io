---
layout: w
title: vue/clii安装踩坑
date: 2019-12-12 20:47:45
tags:
	- vue
categories:
	- 教程
---

### Vue脚手架搭建

#### 1 Vue简介

#####       现在Vue作为最火的前端开发框架，具有入门快，效率高等特点，广受互联网公司的喜爱，纷纷使用和推荐Vue框架来做前端的开发与设计

#### 2 安装vue/cli脚手架

```shell
$ npm install @vue/cli -g
```

如果全局安装过旧版本的vue-cli（1.x或者2.x)需要先卸载旧版的vue-cli(Vue3与旧版本不兼容)

```shell
$ npm uninstall vue-cli -g 
//或者yarn global remove vue-cli
```

![vue-cli](https://upload-images.jianshu.io/upload_images/5814981-fd406123ad261b9f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/939/format/webp)

<u>可以看到我之前的版本是2.9.6，卸载成功后，vue命令便不存在了</u> 

<!--more-->

另外，Vue-Cli 3 需要nodejs的版本>=8.9

```shell
$ node -v(查看node版本信息)
```

![node](https://upload-images.jianshu.io/upload_images/5814981-a9d6d36fc8564b44.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/516/format/webp)

#### 3.安装@vue/cli 	

```shell
$ cnpm install -g @vue/cli 
//或者yarn global add @vue/cli 
```

![@vue/cli](https://upload-images.jianshu.io/upload_images/5814981-3d5dfb1fb27d5689.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/677/format/webp)

#### 4.查看Vue版本

![vue](https://upload-images.jianshu.io/upload_images/5814981-97dc60d5a8968aab.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/677/format/webp)

#### 5使用Vue新建项目

```shell
$ vue create my-pro
//文件名 不支持驼峰（含大写字母）
```

#### 默认选项后，成功新建项目demo

```shell
$ cd my-pro
$ npm run serve
```

![run](https://upload-images.jianshu.io/upload_images/5814981-0c45fee0960e693f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/547/format/webp)

#### 6 查看运行结果

![8080](https://upload-images.jianshu.io/upload_images/5814981-e532bc879ad294ef.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/767/format/webp)

#### 7 踩坑实例

有时会安装@vue/cli出现错误，使用

```shell
$ npm i npm -g (更新npm版本)
$ npm i cnpm --registry=https://registry.npm.taobao.org
$ cnpm i -g @vue/cli
```

**使用以上命令更新镜像源，使用淘宝镜像源来安装下载（国内）**

#### 8 拉取2.x模板

##### Vue CLI 3 覆盖了旧版本的`vue` 命令，如果需要使用旧版本的 `vue init` 功能，可以全局安装一个桥接工具： 

```shell
$ npm install -g @vue/cli-init //`vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
$ vue init webpack my-project
```

#### 9 安装插件

##### ***官方提示：***`vue add` 的设计意图是为了安装和调用 Vue CLI 插件。这不意味着替换掉普通的 npm 包。对于这些普通的 npm 包，你仍然需要选用包管理器 ！

***官方警告：*我们推荐在运行 `vue add` 之前将项目的最新状态提交，因为该命令可能调用插件的文件生成器并很有可能更改你现有的文件。** 

```shell
$ vue add @vue/eslint 
//如果不带 @vue 前缀，该命令会换作解析一个 unscoped 的包，你也可以基于一个指定的 scope 使用（eg：vue add @foo/bar）
```

#### 10 图形化界面

```shell
$ vue ui
```

![ui](https://upload-images.jianshu.io/upload_images/5814981-e93d4fca9ff20679.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/549/format/webp)

![img](https://upload-images.jianshu.io/upload_images/5814981-b51ecf3e250c645e.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/684/format/webp)

![img1](https://upload-images.jianshu.io/upload_images/5814981-40447e81043f981e.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/643/format/webp)

![img2](https://upload-images.jianshu.io/upload_images/5814981-18a81fa7ca54212b.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/643/format/webp)

![img3](https://upload-images.jianshu.io/upload_images/5814981-4bfb10a6bb59934f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/289/format/webp)

![img4](https://upload-images.jianshu.io/upload_images/5814981-12ca22daf4d36d3e.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/564/format/webp)

***安装完成：*你可以在这管理（安装、删除）插件、运行并分析你的项目文件** 

![img5](https://upload-images.jianshu.io/upload_images/5814981-ff86292f519d23a8.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1042/format/webp)

```
文章来源：https://my.oschina.net/wangnian/blog/2051369
```

