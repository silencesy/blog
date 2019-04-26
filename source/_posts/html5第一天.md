---
title: html5基础一
categories: ['前端']
tags: ['html5']
---
###1，严格模式strict.dtd。
>在js开头处加"use strict";就成为严格模式

###2，var fra = document.createDocumentFragment();创建文档碎片。
>document.body.appendchild(fra);

###3，cc:ie6（ie专用注释）

###4，自执行函数(function(){})();

###5，itemscope(那个元素设置了这个属性，就把他当做一个整体)itemprop等

6，guoxiang1991.github.io

7，
<label for="">
	课程：<input type="text" list="course">
<label>
<datalist id="course">
	<option value="php">php</option>
</datalist>

8，广告页必须要小，就可以用到html5的dom操作。

9，html5表单：
9.1 fieldset 元素可将表单内的相关元素分组
9.2 legend标签为 <fieldset>、<figure> 以及 <details> 元素定义标题。
9.3 required 必填项。
9.4 multiple 属性规定输入域中可选择多个值。
9.5 autofocus 默认获取焦点。
9.6 placeholder 占位符。
9.7 pattern 自定义验证。
9.8 min 最大值。
9.9 max 最小值。
9.10 progress进度条
9.11 meter 度量器  使用范列     <label for="">
           入学成绩: <input type="number" max="100" id="score" min="0" step="1" value="0"/>
        </label>
        <label for="">
            基础水平: <meter min="0" max="100" low="60" high="80" value="0" id="level" ></meter>
        </label>
        var score = document.getElementById("score");
        var level = document.getElementById("level");
        score.oninput = function () {
            level.value=this.value;
        }
9.12 <label for="">
            所属学院: <input type="text" list="xueYuan" placeholder="前端与移动开发学院"/>
            <datalist id="xueYuan">
                <option value="前端"></option>
                <option value="移动开发"></option>
                <option value="Java"></option>
            </datalist>
        </label>

10，音乐添加
<audio src = "路径"></audio>autopaly(自动播放 controls 是否显示默认播放控件  loop循环播放)
多浏览器支持方案
<audio controls>
	<source src"路径加不同格式的音乐">
	<source src"路径加不同格式的音乐">
	<source src"路径加不同格式的音乐">
</audio>

11，视频添加
<video src="路径"></video>
autoplay 自动播放
controls 是否显示默认播放控件
loop 循环播放
width 设置播放窗口宽度
height 设置播放窗口的高度（查询浏览器支持情况）
多浏览器支持的方案
<audio controls>
	<source src"路径加不同格式的音乐">
	<source src"路径加不同格式的音乐">
	<source src"路径加不同格式的音乐">
</audio>

12，语义化标签
header头部
container主体部分
article文章
aside侧旁栏
footer底部
section区块

13，表单元素
<datalist>	数据列表
<keygen>	生成加密字符串
<output>	输出结果
<meter>	0度量器

14，兼容处理：在不支持HTML5新标签的浏览器里，会将这些新的标签解析成行内元素（inline）对待。所以我们只需要将其转换成块元素即可使用。但是在IE9版本以下，并不能正常解析这些新标签，但是却可以识别通过document.createElement('tagName')创建的自定义标签，于是我们的解决方案就是将HTML5的新标签全部通过document.createElement('tagName')来创建一遍，这样IE低版本也能正常解析HTML5新标签了，但在实际开发中我们更多采用的是通过检测IE浏览器的版本来加载第三方的一个JS库来解决兼容问题，这个库文件会帮自动通过document.createElement('tagName')创建所有HTML5的新标签。
 
15，微数据
<div itemscope itemtype="http://schema.org/Movie">
		<span itemprop="actor">刘德华</span>
		<span itemprop="director" datatime="2012-02-06T22:30:30.50+08:00">2012年2月6日 22:30</span>
		<!--<a href="" itemprop="url"></a>-->
		<p itemprop="url" >http://www.baidu.com</p>
		<span itemprop="description">评论内容</span>
	</div>


**dom**
1，document.querySelector('selector')通过CSS选择器获取元素，符合匹配条件的第1个元素。

2，document.querySelectorAll('selector') 通过CSS选择器获取元素，以伪数组形式存在。

3，类名操作
1、Node.classList.add('class') 添加class
2、Node.classList.remove('class') 移除class
3、Node.classList.toggle('class') 切换class，有则移除，无则添加
4、Node.classList.contains('class') 检测是否存在class
Node指一个有效的DOM节点，是一个通称。
5，自定义属性
假设某元素<div id="demo" data-name="itcast" data-age="10">
var demo = document.querySelector('#demo');
1、读取 demo.dataset['name']
2、设置demo.dataset['name'] = 'web developer'

