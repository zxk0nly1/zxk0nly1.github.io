---
title: Twilio的node案例
date: 2020-02-14 17:56:41
tags:
	- twilio
	- node
categories:
	- 教程
---

### Twilio + Node 测试

**目的：**使用 twilio 给你的手机发短信

##### `Twilio`是一个位于加利福尼亚的云通信 (PaaS) 公司。Twilio 允许开发者通过使用它提供的 API 进行编程来接电话，收发短信等。 

###### 先来看一下效果图 

![sms](https://img-blog.csdn.net/20161001223207263)

再来看一下代码，是不是很少啊 

```javascript
from twilio.rest import TwilioRestClient

# 下面认证信息的值在你的 twilio 账户里可以找到
account_sid = "ACXXXXXXXXXXXXXXXXX"
auth_token = "YYYYYYYYYYYYYYYYYY"
client = TwilioRestClient(account_sid, auth_token)

message = client.messages.create(to="+8615912345678",  # 区号+你的手机号码
                                 from_="+15555555555",  # 你的 twilio 电话号码
                                 body="Do you know who I am ?")
```

<!--more-->

# 一、安装 twilio

```shell
# npm install twilio --save
```

# 二、注册 twilio

###  2.1. 打开网址 [https://www.twilio.com](https://www.twilio.com/) 

##### 选择`Get a free API key` 

![twilio](https://img-blog.csdn.net/20161001224252482)

### 2.2. 注册信息中，公司名称是可选的，其他的填写上

![register](https://img-blog.csdn.net/20161001224440869)

## 2.3. 验证部分

###### 填写你的手机号后，可以通过`短信`验证，也可以选择`call you insteaded`进行电话验证。 

![phone](https://img-blog.csdn.net/20161001224642339)

### 三、使用

注册成功后，就来到了控制台面板。

#####  记下`ACCOUNT SID`和`AUTH TOKEN`，程序里面要用到。

######  然后`Get Started`，会获得你的 twilio 电话号码。 

![start](https://img-blog.csdn.net/20161001224725121)

按照代码中注释部分填写你对应的值和手机号等等，然后运行看看吧~

你可以用 **twilio** 打电话，也可以用你的手机给 **twilio** 发短信呢。

##### 比较实用的场景：

1. 监控你服务器的情况，如果程序或服务器发生什么事情，可以及时短信通知你。
2. 写一个报警程序，结合传感器，监控家里的情况然后通知你。

### 四、参考文献

##### https://www.twilio.com/docs/

P.S. 说句题外话，在技术翻天覆地的今天，物联网是个大趋势。

使用手机远程控制家里的电器也早已不再是科幻电影里面的场景了，

在回家的路上下达指令，提前把热水烧好，把空调打开。想想多美好 ^_^