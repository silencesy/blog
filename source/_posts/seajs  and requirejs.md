---
title: seajs和requirejs
categories: ['前端']
tags: ['模块化开发']
---
## 为什么要使用模块化
1. 全局变量、全局函数，容易造成变量名冲突
2. 页面引入了一堆的js文件，存在先后顺序的问题
	+ 代码由于组织混乱很容易出错
	+ 出错了很难调试
	+ 后期难以维护
3. 模块化的好处
	+ 提升开发效率
	+ 便于后期维护

## 模块化理解
模块化是一种组织代码的方式，当我们的项目越来越复杂的时候，如果把很多功能业务逻辑写在一起，就会造成开发起来十分的繁琐(因为经常会遇到变量命名冲突、文件依赖过于混乱的问题)，同时维护起来也十分的麻烦，这时候，我们可以考虑把代码按照功能等方面把整个项目划分成一个一个的模块，这样，当我们开发的时候，我们每次只需要关注这一小功能点是如何实现的，从而简化了开发的难度，这样可以提高我们开发的效率，同时，后期维护起来也会变得更加的简单。

#### cmd规范特性
- 一个模块就是一个单独的文件
- 由于每个模块都是属于define关键字函数的回调函数被调用，每个模块都是一个单独的作用域
- 预加载、懒执行（预加载就是预先把所有的模块全部加载完，懒执行就是需要执行哪块才执行哪块）

#### 关键字
- define	定义一个模块
- require	加载一个模块
- exports	暴露一个模块
- module	模块

#### 注意点
- define(function(require,exports,module){});这里面的require,exports,module三个参数的名字是固定写法，不能简写，顺序不能错了 记忆方法：rem
- 如果define里的参数想省略，只能从后面开始省略，只要写了后面的，前面的必须要写上 --> 推荐写全，不要省
- 如果一个模块既不需要公开成员变量，也不需要依赖第三方模块，那么可以全部省略
- seajs.use("入口模块")可以加回调函数，形式如：seajs.use("入口模块",callback);

#### 路径问题

1. 在sea.js当中，js/main和./js/main的含义不是一样的
	+ js/main代表的是在sea.js所在的文件为基准去找，所以找到的是 --> SEAJS所在的父级文件夹/js/main.js 这样的话会找不到的(相对seajs包的路径)
	+ ./js/main代表的是以当前html文件去找js文件夹下面的main.js
	+ require("xxx") --> 其实这里的xxx叫模块标识，不是路径

2. config的作用就是为了简化调用模块
	+ base 设置路径
	+ alias 设置模块的别名，简化调用



## seajs使用
#### 1. 引包 
	<script src="js/sea.js"></script>
#### 2. 入口模块 
	//为了简洁，路径最好不加.js
	//加载完成后触发回调函数
	//简化调用模块
	seajs.config({
	//base 设置路径
	//alias 设置模块的别名，简化调用
		base:"./js"
		alias:{	
			m:"main"
		}
	})
	seajs.use("./js/main",function(){ 
	  console.log('代码执行成功');
	});
#### 3. 主模块
	// 名字写全 并且顺序和单词都要写对（便于记住rem）
	define(function (require, exports, module) {
	// require 方法得到的就是指定的模块中向外暴露的接口对象 	module.exports
	// var fooModule = require('./foo')
	// console.log(fooModule.foo)
	var foo = require('./foo')
		console.log(foo)
	});
#### 4. 第三方模块
	define(function (require, exports, module) {
	// 每个文件模块都是一个模块作用域，外部是无法直接拿到的里面的东西的
	var foo = 'bar';
	// 默认情况下 module.exports 就是一个空对象
	// module.exports.foo = foo
	
	module.exports = 'bar';
	});

#### sea.js把非cmd模块转换成cmd模块
		// 判断的左右就是防止jquery不作为cmd模块使用的时候也可以用
		if (typeof define === 'function' && define.cmd) {
			define(function(require,exports,module){
				module.exports = jQuery;
			});
		}

## require.js
#### 引包
	//data-main引入主模块包
	<script src="js/lib/require.js" data-main="js/app/main"></script>


	//如果想用jQuery,则必须配置如下：
    require.config({
      baseUrl:'./js/app/',//这里设置的是main的路径
      paths:{
        "jquery":"../lib/jquery"
      }
    });

#### main
	//类似angular
	//['./cal']映入第三方模块
	requirejs(['./cal'],function(calculator){
			
			});
#### 第三方模块
	define(function(){
		//用return 提供接口暴露数据
		return 
	});