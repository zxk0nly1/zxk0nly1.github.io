---
title: 使用node写接口
date: 2019-12-12 22:52:10
tags:
	- node
categories:
	- 教程
---

# node简单接口

1. ### 使用npm命令新建package.json文件

```shell
$ npm  init (生成json)
```

2. ### 输入相关信息(index.js->server.js)

3. ### 下载express模板

   ```shell
   $ npm install express
   ```

4. ### 用vscode新建并打开server.js

```js
const express=require("express")
const app=express();

app.get("/",(req,res)=>{
    res.send("hello world！");
})

const port=process.env.PORT || 5000;

app.listen(port,()=>{
    console.log(`Server running on port ${port}`);
})
```

5. ### 使用命令行运行server.js

   ```shell
   $ node server.js
   ```

6. ### 安装nodemon(Node自动重启工具)

```shell
$ npm install nodemon -g --verbose
```

**注意： ** nodemon运行 提示错误时，管理员身份使用powershell

```powershell
$ set-ExecutionPolicy RemoteSigned
```

![powershell](https://img2018.cnblogs.com/blog/992473/201909/992473-20190912143440135-985998266.png)

**选择A 或者 Y**就能执行<u>nodemon</u>了,打开浏览器，输入

```http
http://localhost:5000
```

这个简单的接口就写好了~

