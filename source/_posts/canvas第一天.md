---
title: canvas 基础一
categories: ['前端']
tags: ['canvas'] 
---
#### 1.canvas:canvas是一个H5的标签，它相当于是一张“画布”，我们可以在这一张画布上进行绘制。

#### 2.canvas默认的大小是宽300px，高150px，
	宽度和高度可以通过canvas标签的height和width属性进行设置
	<canvas width='600px' height="300px" >
	注意：请不要使用css来设置canvas的宽度和高度 

#### 3.如何使用canvas进行绘图，步骤如下：
	A.获得canvas标签对象：  var cas = document.getElementsByTagName("canvas")[0];
	B.获取canvas标签对应的绘图工具： var ctx = cas.getContext("2d");
					 var ctx2 = cas.getContext("webgl");
				         var ctx3 = cas.getContext('experimental-webgl');
	C.开始使用绘图工具进行绘制： ctx.moveTo(100,100);//将绘图工具定点在坐标x100，y100的地方
				     ctx.lineTo(200,100);//将绘图工具从100,100的坐标绘制一条到200,100坐标的线（注意，这里的moveTo和lineTo都是打草稿，必须通过stroke或者fill进行真正的绘制）	
	D.真正的绘制图形：    ctx.stroke();//画线
			      ctx.fill();//填充

#### 4.canvas的坐标系：以canvas画布的左上角作为坐标系的原点
	原点向右为x的正方向，原点向左为x的负方向
	原点向下为y的正方向，原点向上为y的负方向

#### 5.fill方法的特性：当我们使用绘图工具绘制图形的时候，如果绘制图形的时候没有将结束的点（lineTo的最后的那个点）和开始的点进行连接，fill方法会自动将结束的点和开始的点进行连接，然后往图形中进行填充。

#### 6.非零环绕原则：判断绘制的图形是否要进行填充的准则。
	从是否要填充的区域拉出一条辅助线来到图形的外面
	如果绘制图形的线穿过辅助线的时候是正方向就记做+1
	如果绘制图形的线穿过辅助线的时候是负方向就记做-1
	最后把所有记录的值加总，如果值为0这块区域就不填充，如果值为非零，这块区域就要填充。
	注意：从左到右为正，从右到左为负。，、

	练习：将回字型的图形绘制出来。

#### 7.closePath方法：可以将绘制的图形进行完美的闭合

#### 8.api集合：
	属性：	ctx.lineWidth = "10";//设置绘图工具画的线的宽度为10px
	      	ctx.lineCap = 'butt';//可以设置的值："square","round";
	      	ctx.lineJoin = 'miter';//可以设置的值："round", "bevel";
		ctx.lineDashOffset = 10;//这个属性可以用来设置虚线的缩进
		ctx.strokeStyle = 'red';//设置描边线条的颜色
		ctx.fillStyle = 'blue';//设置填充的颜色

	方法：	ctx.moveTo(x,y);//将绘图工具进行定点
  	      	ctx.lineTo(x,y);//将绘图工具移动到x，y的坐标
	      	ctx.stroke();//将图形进行描边
	      	ctx.fill();//将图形进行填充
 	      	ctx.closePath();//将图形进行闭合
	      	ctx.beginPath();//开启新路径，开启一个新的绘图状态。
		ctx.setLineDash(数组);//根据数组来设置实现和虚线的绘制
		ctx.getLineDash();//这个方法可以获取一个数组，数组就是设置虚线的数组

#### 9.取消锯齿美化操作：当我们使用canvas进行绘图的时候，为了让图形看起来更加的美观，canvas会做取消锯齿（除了原本绘制的线以外，还会给这根线添加一条更淡颜色的辅助线）。
	取消锯齿的美化操作会在什么时候发生：设置的线宽为奇数的时候，当你画的线不是一个直线的线（倾斜的线。）

	注意：当线宽设置的比较宽了以后，要注意一个事情。线的起始点是从线的线中心开始计算起始点的。

	总结：如果要闭合一个图形，请使用closePath方法，不要再用lineTo连线。

#### 10.开启新路径：beginPath()：用来绘制新的图形内容，此时这个图形内容跟之前绘制的图形没有关系。不会造成图形之间的干扰

#### 11.绘制虚线：
	A.ctx.setLineDash(数组);//根据数组来设置实现和虚线的绘制
	B.ctx.getLineDash();//这个方法可以获取一个数组，数组就是设置虚线的数组
	C.ctx.lineDashOffset = 10;//这个属性可以用来设置虚线的缩进


#### 12.坐标轴的原点转换：
	x0,y0 : 指的是绘制的坐标系的原点
	x,y: 计算出来的坐标点的x,y坐标
	
	var x = (cas.width - paddingLeft - paddingRight - arrowHeight)/2,
	    y = (cas.height - paddingTop - paddingBottom - arrowHeight)/2;

	//转换坐标原点的公式： x = x0+x; y = y0 - y;
	x = x + x0;
	y = y0 - y; 