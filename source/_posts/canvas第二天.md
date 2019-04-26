---
title: canvas基础二
categories: ['前端']
tags: ['canvas'] 
---
#### 1. 绘制折线图
	假设有点: ( 10, 20 ), ( 15, 13 ), ( 17, 30 ), ( 30, 10 ), ( 20, 15 )
	将这些点绘制到坐标轴中.

#### 2. 绘制形状
	-> 矩形
		ctx.rect( x, y, width, heigth )		描边, 需要 stroke 或 fill
		ctx.strokeRect( x, y, w, h )
		ctx.fillRect( x, y, w, h )
		ctx.clearRect( x, y, w, h ) 		清除该矩形区域的内容

	-> 清除整个画布
		ctx.clearRect( 0, 0, cas.width, cas.height );

		cas.width = cas.width;

	-> 圆弧
		ctx.arc( x, y, r, startAngle, endAngle, clockwise )
		ctx.arcTo() 了解
		参数:x,y圆心 r半径，startAngle起始弧度，endAngle结束弧度，clockwise画圆方向（顺时针或者你时针）
	-> 圆
		ctx.arc( x, y, r, 0, 2 * Math.PI )


#### 3. 弧度制
	为了更好的计算角度, 我们该角度提供一个新的定义, 用 PI 作为单位
	将单位圆的一个整圈( 360 度 )记作 2 倍 的 PI.

	这样的度量表示就是弧度制的表示方法.

	60 度 PI / 3
	45 度 PI / 4
	30 度 PI / 6

	学会进行转换

	2 PI 刚好是一圈
	一圈又是 360 度

	2 PI 比上 360 度 = 弧度 比上 对应的角度

	angle 角度
	radian 弧度

	function toAngle ( radian ) {
		return radian * 180 / Math.PI; 
	}
	function toRadian ( angle ) {
		return angle * Math.PI / 180;
	}

#### 4. 角度的坐标
	水平向右的角度是 0 度, 或 0 弧度
	顺时针是正方向, 逆时针是负方向

	练习: 绘制出, 圆心在 canva 正中心, 半径为 100, 角度从 -60度 到 120 度的圆弧

#### 5. 如果没有当前位置, 绘制圆弧是没有任何问题
	但是如果有了当前位置, 绘制圆弧的时候会将当前位置连接到圆弧上

#### 6. 计算在圆弧上的点的坐标

#### 7. 根据固定到起始点到 圆心, 结合圆弧和 closePath 方法可以绘制扇形( 楔形 Wedge)

#### 8. 动态的通过动画, 一点一点的添加角度, 然后绘制一整个圆

#### 9. 绘制文字
	ctx.fillText( 文本内容, x, y )
	ctx.strokeText( 文本内容, x, y );

	常用的属性
	ctx.font = '30px 黑体'

	ctx.textAlign		left, center, right.	start, end
	ctx.textBaseline	top, middle, bottom.	hanging, ideographics, alphabetic

	ctx.measureText( 文本 )		获取当前文字的字体设置下, 文字的宽度对象




1. 绘制矩形的方法：
	A.rect(x,y,width,height);//rect方法只是打草稿，必须配合stroke()或fill()方法来绘制图形
	B.strokeRect(x,y,width,height);//绘制空心矩形
	C.fillRect(x,y,width,height);//绘制填充矩形。

2. 清除矩形区域：
	//擦除从x,y坐标开始的矩形区域，这个区域的大小由width，height来决定
	ctx.clearRect(x,y,width,height);

3. 清除整个画布的内容：
	A.  ctx.clearRect(0,0,canvas.width,canvas.height);
	B.  canvas.width = canvas.width;

4. 绘制圆弧的方法：
	A.
	ctx.arc( 圆心坐标x,圆心坐标y, 圆弧的半径，圆弧开始的弧度,圆弧结束的弧度,圆绘制的方向 );
	ctx.arc(100,100,50,0,2*Math.PI,true);

	ctx.stroke();

	B.
	ctx.moveTo(x0,y0);
	ctx.arcTo(x1,y1,x2,y2,半径);
	//从x0,y0的点拉一条线到x1,y1  再从x1,y1拉一条线到x2,y2.
	//以半径绘制两条线的相切圆。
	

5. 弧度制：为了能够更好的表示的角度，
如果是360度就记做  2*PI

6. 圆弧的0度角在圆心水平向右。
  0度角顺时针是角度的正方向
  0独角逆时针是角度的逆方向

7. 当我们绘制圆弧的时候，有一个特性：
	会将圆弧的起始点和moveTo的定点连接起来

8. 计算圆弧上坐标点的公式：
	x = 圆心坐标x + 半径 * Math.cos(   toRadian(角度));
	y = 圆心坐标y + 半径 * Math.sin(   toRadian(角度));

9. 绘制扇形的步骤：
	A.moveTo到圆心
	B.绘制圆弧
	C.ctx.closePath()


10. 数据饼形图：


11. 绘制文本的方法：
	A.ctx.fillText(文本字符串,x,y);
	B.ctx.strokeText(文本字符串,x,y);

注意：绘制的文本字符串会绘制在x,y坐标处，文字内容左下角对齐x,y坐标点。

设置绘制文字的尺寸：
	ctx.font = "30px 黑体";
设置绘制文字的水平对齐：
	ctx.textAlign = 'left';//left,center,right
设置绘制文字的垂直对齐：
	ctx.textBaseline = "top";//top,middle,bottom






























