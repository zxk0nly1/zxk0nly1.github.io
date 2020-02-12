---
title: eclipse自动补全
date: 2019-12-30 20:08:44
tags:
	- eclipse
categories:
	- 教程
---

#### 1、打开Eclipse，点击“Window - Perfences";

![perfences](https://img-blog.csdn.net/20161217141203508?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJsaWFuMTk5Mg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### **2. 在目录树上选择"Java——Editor——Content Assist"，在右侧的"Auto-Activation"找到"Auto Activation triggers for java"选项;** 

![editor](https://img-blog.csdn.net/20180121205904456?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU2hhdW5fR3Vv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

<!--more-->

#### **3. 在"Auto Activation triggers for java"选项中，默认触发代码提示的就是"."这个符号。将"."后面加入所有的英文大小写字母，更改：.abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ**  

![trigger](https://img-blog.csdn.net/20180121205938587?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU2hhdW5fR3Vv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### **4.更改完成后就可以使用快捷键，迅速敲代码了。** 

![quickcode](https://img-blog.csdn.net/20180121210040250?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvU2hhdW5fR3Vv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

#### 5、其他语言的自动补全，类似，如xml文件自动补全

```shell
在最上端的Auto Activation中将Prompt when these characters are inserted后面的文本框中

的“<=:”替换成“<=:abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ ”（注意后面还有一

个空格）
```



![xml](https://img-blog.csdn.net/20161217141747218?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJsaWFuMTk5Mg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

![quick](https://img-blog.csdn.net/20161217141931406?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZXJsaWFuMTk5Mg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

####  *这样的话我们使用起来就会方便很多。*