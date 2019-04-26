---
title: css3 知识汇总
categories: ['前端']
tags: ['css']
---
### 如何使用手册
#### 学会使用工具，可以让我们事半功倍。
1. []表示全部可选项
2. ||表示或者
3. |表示多选一
4. ？表示0个或者1个
5. *表示0个或者多个
6. {}表示范围
### 一、选择器
  1. 属性选择器：
    --ele[attr]  选取包含这个属性的元素
    --ele[attr=value]  选取这个attr属性有且只有value这一个值的元素
    --ele[attr^=value]  选取这个attr属性中以value字符开头的元素
    --ele[attr$=value]  选取这个attr属性中以value字符结尾的元素
    --ele[attr*=value]  选取这个attr属性中以包含value字符的元素
    --ele[attr~=value]  选取这个attr属性中有value这个属性值的元素
  2. 伪类选择器：
    --ele:first-child  选取当前元素的父级下的第一个子元素
    --ele:last-child  选取当前元素的父级下的最后一个子元素
    --ele:nth-child(xn+y)  选取当前元素的父级下的第xn+y个子元素
    --ele:nth-last-child(xn+y)  选取当前元素的父级下的倒数第xn+y个子元素
    --ele:empty  选取当前元素下没有任何子元素或文本的元素（注释不算，但是空格算 通常用在购物车计数）
    --ele:not(.class)  选取的是除了这个元素之外的元素
    --ele:target  处在锚点状态下的元素（也就是当前元素被锚点状态）
    --ele:checked  选取的是当前处在checked状态下的元素（用于input标签中的单选和复选框）
    --ele:enabled  选取的是当前处在enabled状态下的元素（用于按钮）
    --ele:disabled  选取的是当前处在disabled状态下的元素（用于按钮）
  3. 伪元素选择器：
    --ele:before/ele::before  在当前元素下添加一个before伪元素处在当前元素下最开始的位置
    --ele:after/ele::after  在当前元素下添加一个after伪元素处在当前元素下最末尾的位置
		element::before/element::after {
			content:''; 这里可以填内容  通常为空(如果设置文本内容,则会在该伪元素上显示文本内容)
			display:block;  新建的伪元素是一个行内元素,在使用的时候通常转换为块级元素,但是不一定要转换(也可以通过定位或者浮动来改变成块级元素)
			width:;
			height:;
			...
		}


    --ele::first-letter  当前文本的首字母（也可以是第一个字）
    --ele::first-line  当前文本的第一行（是相对的）
    --ele::selection  设置选中区域的样式(可以设置字体颜色和背景颜色等,但是不可以改变字体大小)
    --input::-webkit-input-placeholder{}选中input里的placeholder并设置样式
	注意:伪元素选择器前面的两个点最好写成一个,以为现在的浏览器默认会添加成两个.
	4. 小技巧
	-webkit-user-select:none;当前元素下的文字不可选中

### 二、颜色
  1. color属性可以赋什么值
    -- red  直接写代表颜色的英文单词
    -- #CCCCCC  16进制表示方法
    -- rgb(0,0,0) 三个参数值分别是0-255，0-255，0-255
    -- rgba(0,0,0,0) 四个参数值分别是0-255，0-255，0-255,0-1最后一个参数表示透明度，不会被其子盒子继承
    -- hsl(0,0%,0%) 三个参数值分别是0-360，0%-100%，0%-100%
    -- hsla(0,0%,0%,0) 四个参数值分别是 色调0-360,饱和度0%-100%(但这个参数为0的时候,必须为0%才不会出错)，亮度0%-100%,0-1最后一个参数表示透明度，不会被其子盒

子继承
	
    -- transparent 完全透明的意思，不可以调节透明度
  2. opacity  表示透明度的意思，取值为0-1之间的数字，会被子盒子继承

### 三、文字阴影
  1. text-shadow: 0px 0px 0px red  文字阴影
    -- 第一个参数表示阴影左右移动的距离（正值向右，负值向左）
    -- 第二个参数表示阴影上下移动的距离（正值向下，负值向上）
    -- 第三个参数表示阴影的模糊度，不能为负值，数值越大阴影越模糊
    -- 第四个参数表示阴影颜色
   (后面可以在用逗号,在添加一个文字阴影.)
### 四、边框
  1. border-radius: 0px 0px 0px 0px / 0px 0px 0px 0px  边框圆角（可以是正圆角也可以是椭圆角，当X/Y轴半径不一样的时候即为椭圆角，如果X/Y轴半径一样，那么“/”后

面的值可以省略不写）
    -- 0 0 0 0 / 0 0 0 0;  标准写法  分别表示1、2、3、4 位置的X/Y轴半径
    -- 0 0 0 / 0 0 0; 简写  分别表示 1、2/4、3 位置的X/Y轴半径
    -- 0 0 / 0 0; 简写  分别表示 1/3、2/4 位置的X/Y轴半径
    -- 0 / 0; 简写  表示四个位置的X/Y轴半径
  2. box-shadow: 0px 0px 0px red  盒子阴影
    -- 第一个参数表示阴影左右移动的距离（正值向右，负值向左）
    -- 第二个参数表示阴影上下移动的距离（正值向下，负值向上）
    -- 第三个参数表示阴影的模糊度，不能为负值，数值越大阴影越模糊
    -- 第四个参数表示阴影颜色
  3. border-image: url("") 27 stretch repeat  边框背景图片（复合属性，也可以拆开写）
    -- 第一个参数表示边框背景图片的引入地址
    -- 第二个参数表示引入的图片中以什么样的尺寸来分割成九份
    -- 第三个参数表示X轴方向的填充方式（round，repeat，stretch）
    -- 第四个参数表示Y轴方向的填充方式（round，repeat，stretch）
    -- border-image-source: url("");
    -- border-image-slice: 27 27 27 27 fill;（背景图片裁切尺寸，最后的fill是表示中间内容区域也显示为图片的中间区域，如果不写默认为中间内容区域留白）
    -- border-image-repeat: stretch repeat round;
    -- border-image-width: 20px;
    -- border-image-outside:1/0px;虚拟变大,只是占以前的大小,不会影响旁边的元素 .设置的值有两种, 数字代表扩大自己的倍数 ,具体的像素.
    说明:  stretch拉伸  repeat平铺(两边会被裁剪)   round显示全部浏览器自动调整

### 五、盒模型
  1. box-sizing:border-box （以边框方式计算盒子的大小）
    -- border-box  设置为border-box以后，我们设置的盒子（width/height）即为content+padding+border
    -- content-box  设置为border-box以后，我们设置的盒子（width/height）即为content（默认）
    说明:  默认的box-sizing:content-box;优先保证内容的大小  对盒子进行缩放. box-sizing:border-box;让盒子优先保证自己所占域的大小,对内容进行压缩.
### 六、背景
  1. background-size: 10px 10px  背景图片的尺寸大小（也可以设置为contain、cover）
    --contain  图片两边等比例拉伸，直到某一边顶格停止拉伸（长边位置顶格后，短边位置不再拉伸，其余位置留白）
    --cover  图片等比例拉伸，保证两边都顶格，可能会出去（短边位置顶格，长边位置溢出盒子）
  2. background-position: 10px 10px/top left  背景图片定位
  3. background-origin:  背景图片的开始位置
    --border-box  让图片背景在border开始的位置开始显示
    --padding-box  让图片背景在padding开始的位置开始显示（默认）
    --content-box  让图片背景在content开始的位置开始显示
  4. background-clip:
    --content-box  内容区域以外的背景图片全部裁切掉（不是图片缩小或移动位置，而是直接裁切）
    --padding-box  padding区域以外的背景图片全部裁切掉（不是图片缩小或移动位置，而是直接裁切）
  5. background-image
    --background-image:url(""),url(""),...,...;  多张背景图片以逗号分隔可以引入多张背景图片
    --background-position:top left,top left;当设置了多重背景时要设置背景位置时也用逗号隔开设置,其位置时一一对性的.

### 七、渐变
  1. linear-gradient()  线性渐变
    --第一个参数表示线性渐变的方向（to top/right/bottom/left，也可以是具体的角度360deg）
    --第二个参数表示从什么颜色开始（也可以在颜色后面加上百分比 yellow 25%）
    --第三个参数表示向什么颜色渐变（根据上一个百分比来决定从多少到多少,为什么颜色）
    --第四个参数表示向什么颜色渐变（从第四个开始可以写可以不写）
    --......
  2. radial-gradient()  径向渐变
    --第一个参数表示径向渐变的范围（为半径值）
    --第二个参数表示径向渐变的开始位置（at 渐变开始的位置，也可以是具体的值）
    --第二个参数表示从什么颜色开始（也可以在颜色后面加上百分比 yellow 25%）
    --第三个参数表示向什么颜色渐变（根据上一个百分比来决定从多少到多少为什么颜色）
    --第四个参数表示向什么颜色渐变（从第四个开始可以写可以不写）
    --......
  3. http://www.colorzilla.com/gradient-editor/  自动生成全兼容渐变代码
 具体说明:  
   #### 渐变
   1. 线性渐变
       background-image:linear-gradient(to right,yellow,green);黄色从左到右渐变为绿色
       方向还可以用度数但是要带单位deg 0deg向上 90deg向右
       background:linear-gradient(90deg,yellow 25%,green);开始%25是黄色不开始渐变,过了%25之后才开始渐变(这个百分比相当于       整个盒子)background:linear-

gradient(90deg,yellow 25%,green 50%);
       还可以个多个值:例如  background:linear-gradient(90deg,yellow 25%,green 25%m,pink 50%); 
       方向 颜色 范围
   1. 径向渐变
       有原点(圆心) 两种颜色
       background-image:radial=gradient(120px at center center,yellow,green);
       第一个参数是半径  后面两个是坐标 左后是颜色
       background-image:radial=gradient(120px 80px at center center,yellow,green);
       写了两个半径就是椭圆  后面坐标可以用单词 给百分比 和具体的数值
       background-image:radial=gradient(120px 80px at center center,yellow,green 25%,blue);和线性渐变基本一样
   总结注意:要想不要渐变的效果就这样设置background:linear-gradient(90deg,yellow 25%,green %25,green 50%) ;
### 八、过渡动画
  1. transition: all 1s 1s ease  过渡动画（从其实状态到结束状态的改变，只能是两个这状态的改变）
    --后面参数的书写顺序没有具体规定，不过出现的第一个时间一定是过渡需要的时间，第二个才是延迟时间
    --一般大家默认写成（属性、过渡时间、延迟时间、线性）
    --第一个参数为transition-property  是我们需要的过渡的属性（可以是单一的某一个，如果全部都过渡就写all）
    --第二个参数为transition-duration  是完成本次过渡动画的总时间
    --第三个参数为transition-delay  是本次动画开始是的延迟时间
    --第四个参数为transition-timing-function  是本次动画的动画线性（默认为ease）
  2. http://cubic-bezier.com/#.17,.67,.83,.67  生成过渡线性（贝塞尔曲线）
  说明:动画线性的其他值
     linear： 线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0) 
     ease： 平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0) 
     ease-in： 由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0) 
     ease-out： 由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0) 
     ease-in-out： 由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0) 
    这里注意如果transition: all 1s 1s ease加在element:hover触发的时候就只会执行一次动画   加在element的时候会执行两次动画

### 九、2D转换
  所有2D转换都是transform属性，只不过后面的值不一样
  1. transform: translate  2D转换中的位移
    --translateX(20px) 向X轴正方向移动20px
    --translateY(20px) 向Y轴正方向移动20px
  2. transform: scale  2D转换中的缩放
    --scaleX(1) 延X缩放1倍（1为没有缩放，大于1就是放大，小于1就是缩小，不可为负值，没有单位）
    --scaleY(1) 延Y缩放1倍（1为没有缩放，大于1就是放大，小于1就是缩小，不可为负值，没有单位）
  3. transform: rotate  2D转换中的旋转
    --rotate(360deg)  旋转一定的角度（即在Z轴上旋转，正值为顺时针，负值为逆时针）注意:transform-origin:top right;绕具体位置旋转(值可以为坐标单词和具体的像素值)
  4. transform: skew  2D转换中的倾斜（扭曲）
    --skewX(360deg)  顺着X轴进行倾斜（不常用）
    --skewY(360deg)  顺着Y轴进行倾斜（不常用）
   注意:transform:translatex(x);
          transform:translatex(y);
         上面这样写法,后面会覆盖前面的,当两个都要写的时候就这样写transform:translatex(x) translatex(y);

### 十、3D转换
  1. transform: translate 3D转换中的位移
    --translateX(20px) 向X轴正方向移动20px
    --translateY(20px) 向Y轴正方向移动20px
    --translateZ(20px) 向Z轴正方向移动20px
  2. transform: rotate  2D转换中的旋转
    --rotateX(360deg)  旋转一定的角度（延X轴进行一定的角度旋转）
    --rotateY(360deg)  旋转一定的角度（延Y轴进行一定的角度旋转）
    --rotateZ(360deg)  旋转一定的角度 ( 延Z轴进行一定的角度旋转 )
          注意:transform:rotate3d(1,1,1,45deg)前面三个一 正的正着转 负的反着转
  3. transform-origin: left bottom  改变旋转轴的位置
      第一个参数可以为 top bottom left right
      第一个参数可以为 top bottom left right
      这里的参数还可以设置像素值
  4. transform-style: preserve-3d  设置在父级盒子上，让其子元素在3D效果下
  5. perspective: 600px  进行600px距离的透视效果，距离越大效果越不明显

     注意:我们可以同时使用多个转换，其格式为：transform: translate() rotate() scale() ...等，其顺序会影转换的效果。
            当在设置动画的时候如果元素本身设置了transform的属性时 如translate() rotate();
            那么在hover的时候要与元素本身的transform属性一一对应顺序才能正确的显示
      具体例子
	如:.rocket {
			height: 190px;
			width: 100px;
			position: absolute;
			bottom: 0;
			transform:  translate(0, 0) rotate(30deg)  ;
			transition: transform 1s;
		}
		section:hover .rocket{
			transform:translate(1000px, -500px) rotate(900deg) ;
		}

### 十一、帧动画
  1. @keyframes 名字{}  是指动画的定义阶段，里面会写明动画在各个阶段会变换成什么样子
    --{
       from{
       		from中如果不设置,默认使用的是,初始状态
       	}
       to{
       		to中设置的是结束时的状态
       	}
     }
    --{
       0%{
           	0%中如果不设置,默认使用的是,初始状态
        }
       50%{
            50%中设置的是动画中50%帧位置时的动画，当然也可以写的更加细致
        }
       100%{
           	100%中设置的是结束时的状态
        }
     }
  2. animation-name: 名称; 与我们定义动画的时候名字配套，是指我们本次动画使用我们定义的哪一个动画
  3. animation-duration: 2s; 持续时间，是指我们的本次动画要多少时间完成
  4. animation-delay: 2s; 延迟时间，是指我们的本次动画在最开始的时候延迟多少时间后开始
  5. animation-iteration-count: infinite;  执行次数，是指本次动画执行多少次，infinite为无限
  6. animation-timing-function: linear;  是指动画执行的线性(step(5)分布执行)
  7. animation-fill-mode: forwards;  是指动画结束时的状态
    --backwards：动画开始状态是从动画的第一帧开始而不是原始状态开始，动画结束后回到最原始状态
    --forwards：动画从最原始状态开始，而不是第一帧，动画结束后就留在最后的状态
    --both：动画开始状态是从动画的第一帧开始而不是原始状态开始，动画结束后就留在最后的状态
  8. animation-direction: normal; 是指动画执行的顺序，在多次执行动画时设置
    --normal 是指每次动画都是正向执行
    --reverse 是指每次动画都是反向执行
    --alternate 是指多次动画时以正向开始，并以（正、反、正...）的顺序执行下去
    --alternate-reverse 是指多次动画时以反向开始，并以（反、正、反...）的顺序执行下去
  9. animation-play-state: running; 是指动画的暂停与播放
    --running 是指动画播放
    --paused 是指动画暂停
     (用js暂停动画dom.style.animationPlayState='paused';)
  10. 连写习惯:名称 持续时间 线性 次数 顺序 结束状态 运动和暂停
     连写注意:    复合写法
              1属性的顺序是可以随意调换的
	          2第一次出现的时间是动画持续时间
	          3第二个出现的时间是延迟时间
	          4如果只设置一个时间 默认就是动画持续事件
### 十二、flex弹性盒子
  1. display: flex 设置在父级盒子上，表示开启弹性布局，开启后其子元素会拥有一个主轴，一个侧轴，主轴默认是X轴方向是从左向右，侧轴垂直于主轴，默认方向是从上向下
  2. justify-content: flex-start;  设置在父级盒子上，表示主轴方向上的分布排列
    --flex-start 这是默认值，是从开始位向结束位依次排列
    --flex-end 是从结束位向开始位依次排列
    --center 是居中显示
    --space-between 是从开始位向结束位依次排列，左右顶格，所有元素中间的间隙相等
    --space-around 是从开始位向结束位依次排列，左右不顶格，最左则元素的左边间隙和最右边元素的右边间隙相等，所有元素中间的间隙为左右两侧的二倍
   说明:space-between  左右靠边,中间间歇相等排布,父盒子的宽度减去所有子盒子的宽度除以(盒子-1)让左右盒子的靠边,其他盒子中间就插上刚刚所算出来的值
          space-around左右间歇相等 父盒子的宽度减去所有自盒子的宽度再除以所有盒子*加在每个盒子的两侧
  3. align-items: stretch;  设置在父级盒子上，表示对侧轴方向上的分布排列，这是在只有一行的时候使用
    --stretch 表示其下的子盒子会在侧轴上进行拉伸至上下顶格，会和我们元素本身的宽和高有冲突
    --flex-start 排在开始位
    --flex-end 排在结束位
    --center 是居中显示
  4. align-content: flex-start; 设置在父级盒子上，表示对侧轴方向上的分布排列，这是在多行的时候使用(注意当只有一行的时候无法生效)
    --flex-start 是从开始位向结束位依次排列
    --flex-end 是从结束位向开始位依次排列
    --center 是居中显示
    --space-between 是从开始位向结束位依次排列，左右顶格，所有元素中间的间隙相等
    --space-around 是从开始位向结束位依次排列，左右不顶格，最左则元素的左边间隙和最右边元素的右边间隙相等，所有元素中间的间隙为左右两侧的二倍
  5. flex-direction: row;  改变主轴的方向
    --row 是默认值，是主轴从左到右的方向排列,开始位在最左侧
    --column 是主轴从上到下的方向排列，开始位是最上方
    --row-reverse 是主轴从右到左的方向排列,开始位在最右侧
    --column-reverse 是主轴从下到上的方向排列，开始位是最下方
  6. flex-wrap:nowrap; 是否允许换行
    --nowrap 是不允许换行，是默认值
    --wrap 是允许换行
  7. align-self: flex-start; 设置在子盒子上，是表示当前元素在当前侧轴上所处的位置
    --flex-start 排在开始位
    --flex-end 排在结束位
    --center 是居中显示
  8. order: 1; 设置在子元素上，表示子元素的顺序，按照从大到小的顺序排列，不写的话默认为1
  9. flex: 1; 设置在子元素上，表示子元素在父盒子中主轴方向上所占的比重


### 零碎知识点:
1. -webkit-user-select:none;设置某元素的文字不能被选中.
2. 实现自定义三角形
.box {
     height: 0;
    width: 0;
    border: 50px solid;
    border-color: yellow transparent transparent transparent;
    margin: 50px auto 
}
3. position:absolute;
   top:0;
   left:0;
   right:0;
   bottom:0;
相当于height:100%;width:100%;但是元素必须加绝对定位
4. backface-visibility:hidden;后面隐藏

