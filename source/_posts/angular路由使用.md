---
title: angular路由使用
---
## angular路由使用

#### 安装angular-route
- npm install angular-route --save
#### 引用模块
- `<script src="node_modules/angular-route/angular-route.js"></script>`
#### 创建模块
- `var app = angular.module('myApp',['ngRoute']);`
#### 使用规则
	//有一个参数：类似于controller的第二个参数 

	//需要注入一个参数$routeProvider 这个参数是用来设置具体的规则的

	app.config(['$routeProvider',function($routeProvider){

	// 路由参数：

	// when方法，第一个参数是当前url中锚点值

    // 第二个参数是一个object对象 并且可以通过.实现链式编程  从而实现多个筛选（不过一般使用路由参数动态的实现筛选）

	// 当我们满足这样的规则的时候就会把模板的内容插入到页面插入有ng-view属性的标签的innerHTML

	//路由参数'/students/:name?'这里加?（0-1）个参数 让参数可控 当/后面没有内容的时候也走这个规则

		 $routeProvider.when('/students/:name?',{

				//模板 template/templateUrl

                template:'<p>{{nowStu.id}},{{nowStu.name}},{{nowStu.grade}}</p>',

                // 指向一个控制器的名字 最终我们需要在这个模板中使用一些数据模型

                controller:'stuController'

				//otherwise 当上面的when都没有匹配的时候  就走这里面  需要一个参数 是一个对象

            }).otherwise({

				//当前面所有的when都不满足时  就会跳转到这个指定的锚点值页面

				redirectTo:'/students/'

				})

		 //创建控制器

		 //控制器暴露的数据能够在template中使用

		 //$routeParams是一个对象 获取url中想要匹配的值 如 {name:"zhangsan"}

		 //$route监视url参数的变化 

		app.controller('stuController',['$scope','$routeParams'，'$route',function($scope,$routeParams,$route){

				$scope.students = {

            	zhangsan: {id: 0, name: "张三", grade: "一年级"},

            	lisi: {id: 1, name: "李四", grade: "一年级"},

            	xiaobai: {id: 2, name: "小白", grade: "一年级"},

            	wangwu: {id: 3, name: "王五", grade: "一年级"},

            	zhaosi: {id: 4, name: "赵四", grade: "一年级"},

        		}

			//动态暴露数据 为了让路由中的模板使用

		$scope.nowStu = $scope.students[$routeParams.name];

			//当用户输入的数据没有的时候就会默认跳转到摸个数据上进行显示

			if($scope.nowStu){

				//$scope.nowStu=$scope.students['lisi'];

				//$route提供一个方法 默认会跳转到lish的信息

				//updateParams他只能改'/students/:name?'中name的值

				$route.updateParams({name:'lisi'});

				//如果要改urL整个的值 需要使用$location.url('/sunyu/') 但是注意$location.url获取的锚点值不包括#

				$location.url('/sunyu/')；
			}
		}]);