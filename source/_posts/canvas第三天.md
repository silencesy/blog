---
title: canvas基础三
categories: ['前端']
tags: ['canvas'] 
---
#### 
1. 图片绘制
	创建图片元素
	document.createElement( 'img' )
	var img = new Image();
	img.src = '';资源图片的路径。
	ctx.drawImage()
	有三种调用形式
	1> ctx.drawImage( img, x, y ) 将 image 绘制到 x, y 表示的位置
	2> ctx.drawImage( img, x, y, width, height ) 将 img 绘制到一个矩形区域内
	说明，前面的x，y为绘制起始的位置，后面的width和height是图片显示的大小。
	这里可以使x,y加一个数字实现叠图的效果。
	3> ctx.drawImage( img, sx, sy, sw, sh, x, y, w, h )
		将图片 img 的 sx, sy, sw, sh 部分的内容绘制到画布的x, y, w, h 的矩形区域内.
	说明sx,sy是资源图片的起始位置，sw,sh资源图片的宽高，x,y目标显示起始坐标，目标显示宽高。
	
	
2. 计时器模型
	var id = setInterval(function () {

		if ( 条件 ) {

			clearInterval( id );
		}


		// 继续执行我的内容

	}, 20);
	知识点：ctx.clearRect( 0, 0, cas.width, cas.height );擦除整个画布。
	动画：核心代码参考
	<script>
		function toAngle( radian ) {
			return radian * 180 / Math.PI;
		}
		function toRadian( angle ) {
			return angle * Math.PI / 180;
		}
		var cas = document.getElementById( 'cas' );
		var ctx = cas.getContext( '2d' );
		var img = new Image();
		img.src = 'NPCrabbitbaby-2.png';
		img.onload = function() {
			var width = img.width / 4;
			var height = img.height / 4;
			var i = 0;
			setInterval(function() {
			ctx.clearRect( 0, 0, cas.width, cas.height );
			ctx.drawImage( img, i*width,0,width,height,100,100,width,height);
			if ( i == 3) {
				i = 0;
			} else {
				i++;
			}
		},200);
}

3. 变换的概念
	计算机绘图是利用坐标进行绘图. 绘制任何图形都和坐标系的结构息息相关.

	所谓的变换就是一套数学公式, 可以记录坐标轴的变化方式.
	利用坐标轴的变换可以绘制出, 根据不同坐标轴特点而形成的图形.

	基本的 api
	ctx.translate(x,y)		平移变换
	ctx.rotate(reg)		旋转变换
	ctx.scale(x,y)			伸缩变换


4. 封装绘图对象
	Line
	Rect
	Circle	x, y, radius, strokeStyle, fillStyle, lineWidth
	Arc

	function Line( config ) {

	}
	Line.prototype = {
		stroke: function () {

		}
	}


5. canvas 的状态
	在 Canvas 中凡是设置了属性效果, 都会延续到后面一次修改
	Canvas 在创建出来的时候, 是有一个默认的状态的
	我希望每次修改状态的时候 都是不影响原来默认状态的
	每次画完图时, 我都会新建一个状态, 然后绘制完成后
	恢复到原有状态

	ctx.save()		将当前状态保存
	ctx.restore() 	将保存的状态恢复

	状态栈

6. 在 canvas 绘制的时候允许使用 canvas 绘制 canvas
	
	ctx.darwImage( img, ... )

	此时 img 可以是 图片, 还可以是 canvas, 甚至是 video



7. Konva 是一个完全面向对象的框架
	将所有的东西都看做是对象: 图片, 直线, 矩形, ...
	将整个canvas看做成舞台(stage)
	在舞台上放一个层, 那么将所有的图形放在这个层中


	命名空间

	var num = 123;
	function foo() {}
	// 污染全局作用域
	var Itcast = {};

	Itcast.num = 123;
	Itcast.foo = function () {};

8. 获取当前字体大小的情况下某些文字占用的宽度和高度
	ctx.font = "20px";
	var obj = ctx.measureText("你好");
	obj.width  obj.height

9. 在canvas里面绘制图片：
	A.创建一个图片对象
	  var img = new Image();//创建一个图片对象
	  img.src = '1.jpg';

	B.等图片对象加载完成以后，将图片对象绘制到canvas里面去
	  //等待img对象加载完成以后，执行函数
	  img.onload = function(){
		//1.将图片绘制到canvas里面的坐标0，0处
		ctx.drawImage( img , 0 , 0 );

		//2.将图片绘制到canvas里面的坐标0,0处，并且图片大小为width,height
		ctx.drawImage( img , 0, 0, width, height);

		//3.将图片img的sx,sy坐标处的sw,sh大小的图片区域绘制到canvas里面的x,y坐标处的大小为w,h			//的区域中
		ctx.drawImage( img , sx,sy,sw,sh,  x,y,w,h);
	  }


10. 变换的概念：
	我们现在的canvas绘图都是通过坐标来进行绘制。
	所谓的坐标就是canvas坐标系中的一个点。
	canvas的坐标系可以通过变换来进行改变，当canvas的坐标系发生了改变的时候，坐标点也会跟着发生改变。
	最后我们可以通过变换来画出一些比较好看的图形。


	变换的api方法：
		A.translate(x,y);//平移变换，
		B.rotate(deg);//旋转坐标系，旋转deg度
		C.scale(2,0.5);//缩放变换,  x轴放大2倍，y轴缩小一半








	




















