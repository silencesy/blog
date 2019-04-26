---
title: art-template模板引擎
categories: ['前端']
tags: ['模板引擎']
---

#### jQuery遍历对象
	$.each(data,function(i,e){e.attr})；
	attr就是对象的属性。
	例如：$.each(data,function(i,e){
		var date = new Date(Number(e.time+'000')).toLocaleString();
		infomation += '<ul><li>'+ e.desc +'</li><li>'+ date +'</li></ul>';
	})
#### artTemplate方法一
	<!DOCTYPE HTML>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>basic-demo</title>
	<script src="../dist/template.js"></script>
	</head>

	<body>
	<div id="content"></div>
	<script id="test" type="text/html">
	{{if isAdmin}}

	<h1>{{title}}</h1>
	<ul>
    {{each list as value i}}
        <li>索引 {{i + 1}} ：{{value}}</li>
    {{/each}}
	</ul>

	{{/if}}
	</script>

	<script>
	var data = {
		title: '基本例子',
	isAdmin: true,
	list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
	};
	var html = template('test', data);
	document.getElementById('content').innerHTML = html;
	</script>
	</body>
	</html>
#### artTemplate方法二
	<!DOCTYPE HTML>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>compile-demo</title>
	<script src="../dist/template.js"></script>
	</head>
	
	<body>
	<h1>在javascript中存放模板</h1>
	<div id="content"></div>
	<script>
	var source = '<ul>'
	+    '{{each list as value i}}'
	+        '<li>索引 {{i + 1}} ：{{value}}</li>'
	+    '{{/each}}'
	+ '</ul>';
	
	var render = template.compile(source);
	var data = {
	    list: ['摄影', '电影', '民谣', '旅行', '吉他']
	};
	var html = render(data);
	
	document.getElementById('content').innerHTML = html;
	</script>
	</body>
	</html>

#### artTemplate方法三-嵌入子模板

	<!DOCTYPE HTML>
	<html>
	<head>
	<meta charset="UTF-8">
	<title>include-demo</title>
	<script src="../dist/template.js"></script>
	</head>
	
	<body>
	<div id="content"></div>
	<script id="test" type="text/html">
	<h1>{{title}}</h1>
	{{include 'list'}}
	</script>
	<script id="list" type="text/html">
	<ul>
	    {{each list as value i}}
	        <li>索引 {{i + 1}} ：{{value}}</li>
	    {{/each}}
	</ul>
	</script>
	
	<script>
	var data = {
		title: '嵌入子模板',
		list: ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
	};
	var html = template('test', data);
	document.getElementById('content').innerHTML = html;
	</script>
	</body>
	</html>


#### 注意点
	{{each list as value i}}
	list可以为对象或者是数组，value为值，i为索引。
#### 把获取到的时间转换为现在的时间
	var data = new Date(Number(e.time+"000")).toLocaleString();
	因为从后台传回来的是json格式的字符串，并且new Date().toLocaleString();里面必须为数字。所以用Number强制转换为数字。



