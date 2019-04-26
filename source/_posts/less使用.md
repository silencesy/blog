---
title: less基础语法
categories: ['前端']
tags: ['css预处理器']
---
## less语法
#### 一、注释的区别
	/**/会编译在css文件中
	//不会编译在css中
#### 二、声明变量及使用 
	@maincolor:#92322;
	使用变量 body{ color:@maincolor;}
#### 三、mixin混入
	.redFont{
		color:red;
	}
	.redBorder {
		border:1px solid red;
	}
	//红色文字和边框 通过class混合
	.redFontBorder-class {
		.redFont();
		.redBOrder();
	}
	//方法
	.redFont-func(){
		color:red;
	}
	.redBorder-func(){
		border:1px solid red;
	}
	
	//红色文字和边框 通过func混合
	.redFontBorder-func{
		.redFont-func();
		.redBorder-func();
	}

#### 四、嵌套
	#header{
		width:100px;
		>div{
          width:100px;
			p{
				width:100px;
				&:hover {
					width:100px;
				}
			}
			&+div {
				width:100px;
			}
			//&~div {
				width:100px;
			}
		}
	}
	直接写在里面就是 后代选择器
	&：hover
	> 子代选择器
	&+ 加号选择器
	&~ 波浪选择器

#### 五、导入@import
	注意这里引入less文件的时候不用加后缀名
	如: @import "文件名"；
	可以使用引入文件的变量和函数以及类名。

#### 六、运算
	颜色运算
	@red:red*0.5;
	内置函数
	@gary:darken(#333,10%);

#### 七、less的使用
	引用less文件 注意在引用的时候文件类型写type/less
	引用less.js文件(在浏览器上使用less，我们需要添加一个js插件 less.js 解析less文件动态加载
	注意：他是一部加载less文件　然后解析
	一定要求是　使用http形式访问　否则无法加载less文件
	不建议使用less.js这种形式来用less
