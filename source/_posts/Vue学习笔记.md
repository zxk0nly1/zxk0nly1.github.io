---
title: Vue学习笔记
date: 2019-11-19 22:09:17
tags: vue
category: vue
---
## vue学习笔记
### 开篇语

建议新手学习,请不要用npm的方式(vue-cli,vue脚手架),太复杂了. 请直接下载vue.js文件本地引入,就上手学习吧
参照菜鸟教程网站的vue.js教程https://www.runoob.com/vue2/vue-start.html
从基础开始理解和上手,请看我写的中文注释,帮助理解

### 一些建议
直接把菜鸟教程的例子复制到自己的代码编辑器里看更好

菜鸟教程的好处我觉得之一是其有很多实例子,那么就应该拿例子复制回来本地自己的编辑器看.

因为菜鸟的例子左边代码,右边视图.就很小了,不好审视.

要打开浏览器控制台(比如我们推荐用谷歌浏览器chrome在浏览器按f12就可以打开控制台),

直观的看到js和dom层,比看到界面更重要的是看到dom层的实际操作变化

![vue](https://segmentfault.com/img/bVbcvzG?w=1598&h=918 "vue")

### 一个简单的vue.js例子

	<body>
	 <h2>vue</h2>
	  <div id="myapp">
	   <p title="哈哈">学习vue很舒服</p> 
	   <p>{{ message }}</p> <p>{{ mz }}</p> 
	   </div> 
	   <script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script> 
	   <script type="text/javascript"> 
	   var myapp = new Vue( //新建一个Vue 实例并赋值给变量'myapp',这时变量myapp就是这个vue实例 
	   { 
		   el:'#myapp',
		   data:{ message:'hello Vue',  //myapp.message = 'hello Vue' 
		   mz:'张三33'  //myapp.mz = '张三33' } } 
	   ); 
	   </script> 
	   </body>
<!-- more -->
### vue.js一个简单例子的基础说明系列-[第1个例子]

	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>vue一个简单例子的基础说明</title>
	</head>
	<body>
	<div id="vue_det">
	<!--  {{ }} 用于输出对象属性和函数返回值。  -->
	<h3>site : {{site}}</h3>
	<h3>url : {{url}}</h3>
	<h3>alexa : {{alexa}}</h3>
	<h3>{{details()}}</h3>
	</div>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
	var vm = new Vue({
	el: '#vue_det',//el 参数，它是 DOM 元素中的 id,这意味着我们在该div里面作业,外面不受影响,不会影响外面
	data: {//data 用于定义属性，实例中有三个属性分别为：site、url、alexa。
	site: "菜鸟教程",//这是一个属性site,其值是字符串"菜鸟教程"
	url: "www.runoob.com",//同上
	alexa: "10000"//这是一个属性alexa,其值是字符串"10000"
	},
	methods: {//methods 用于定义的函数，可以通过 return 来返回函数值。
	details: function() {
	return this.site + " - 学的不仅是技术，更是梦想！";
	}
	}
	})
	</script>
	</body>
	</html>

### vue.js一个简单例子的基础说明系列-[第2个例子]---实例属性与方法,它们都有前缀 $

	<!DOCTYPE html>
	<html>
	<head>
	<meta charset="utf-8">
	<title>vue.js一个简单例子的基础说明系列-[第2个例子]</title>
	</head>
	<body>
	<div id="vue_det">
	<h1>site : {{site}}</h1>
	<h1>url : {{url}}</h1>
	<h1>Alexa : {{alexa}}</h1>
	</div>
	<script src="js/vue.min.js" type="text/javascript" charset="utf-8"></script>
	<script type="text/javascript">
	// 我们的数据对象
	//除了数据属性，Vue 实例还提供了一些有用的实例属性与方法。它们都有前缀 $，以便与用户定义的属性区分开来。
	var data = { site: "菜鸟教程", url: "www.runoob.com", alexa: 10000}//定义一个js变量.即js属性
	var xm = '小明';//定义一个js变量.即js属性
	var vm = new Vue({
	el: '#vue_det',//定义一个vue属性el,要使用vm.$el才能访问
	data: data//定义一个vue属性data,要使用vm.$data才能访问
	})
	//       我们在浏览器控制台访问上面的那些变量和属性,直接通过.的方式
	//        document的子是vm,vm的子是el和data,document.vm能访问vm,而vm.el这样写是
										//访问不到vm的,要这样写vm.$el才能访问,因为el是Vue实例的直接子变量
	//       data  ->{__ob__: wr}   //是对象
	// xm   ->'小明'
	// el   ->VM113:1 Uncaught ReferenceError: el is not defined    //这样是访问不了的,因为el不是js的全局变量/属性
	// vm.el   ->undefined    //这样也不行,要写成vm.$el才对
	//       vm.$el   -><div id="vue-det">...</div>    //这样才是访问vue的
	</script>
	</body>
	</html>

