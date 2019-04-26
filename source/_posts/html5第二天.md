---
title: html5基础二
categories: ['前端']
tags: ['html5']
---
1,window.addEventListener

2,onLine "L"大写的时候是一个属性，后面不用加括号，直接调用就行，返回一个布尔值。用法:alert（window.navigator.onLine）;返回浏览器是否联网（boolean值）
onlone "l"小写的时候是一件事件，这个事件只能用dom二级事件来绑定
“navigator”是window上的一个属性，所以写的时候window可以不写，但是建议写上（代码的完整性）
online事件在pc端的时候一定是从离线状态变到上线状态的时候才会触发。

2,判断当前设备状态
2.1 监听设备在线
window.addEventListener('online', function () {
			// alert('online');
			$('.tips').text('网络已连接').fadeIn(500).delay(1000).fadeOut();
		});
delay(时间值)方法 ：是设置延迟时间。

2.2 监听设备离线
window.addEventListener('offline', function () {
			// alert('offline');
			$('.tips').text('网络已断开').fadeIn(500).delay(1000).fadeOut();
		});


3，html全屏 document.documentElement.webkitRequestFullScreen();

任意元素全屏显示
node.webkitRequestFullScreen();（谷歌浏览器加webkit）
node.mozRequestFullScreen();（火狐加moz）
任意元素关闭全屏显示
Node.cancelFullScreen()（理论是这样关闭实际上是用document.webkitCancelFullScreen()关闭）

兼容写法：					function FullScreen(node){
			if (node.mozRequestFullScreen){
				node.mozRequestFullScreen();
			}
			else if(node.webkitRequestFullScreen){
				node.webkitRequestFullScreen();
			}else if(node.msRequestFullScreen){
				node.msRequestFullScreen();
			}else if(node.oRequestFullScreen){
				node.oRequestFullScreen();
			}
		}


4，所有元素只能通过document才能调用关闭全屏
document.webkitCancelFullScreen();

4,检测当前是否处于全屏
document.webkitIsFullScreen
(返回一个boolean值)

5，webkit谷歌浏览器  moz火狐浏览器 msIE浏览器 o欧朋浏览器

6，全屏伪类
		.box:-webkit-full-screen {
			background-color: blue;
		}（当box全屏的时候，box的背景变为蓝色）
:full-screen .box {}、:-webkit-full-screen {}、:moz-full-screen {}

7，状态改变触发事件.change();

8，base64码。

9，拖拽事件：
在HTML5的规范中，我们可以通过为元素增加draggable="true"来设置此元素是否可以进行拖拽操作，其中图片、链接默认是开启的。
页面中任何一个元素都可以成为目标元素，不需要特殊指定

9.1、拖拽元素
dragstart事件 ：一定是点击加位移才会触发
dragend事件 ：一定是位移以后再松开鼠标才会触发
拖拽元素开始拖拽以后他的元素会变成光标，松开鼠标以后他会回到原点这段时间，元素会变成本身大小。
dragleave事件 ：一定是光标离开拖拽元素的时候才会触发。
drag事件 ：只要拖拽开始就一直在不停的触发，直到拖拽结束（期间不管光标是否移动，都会一直触发）

9.2目标元素
dragenter事件 一定是光标进入目标元素的时候才触发
dragover事件 只要拖拽元素在目标元素内就会触发，无论光标是否移动
drop事件 在目标元素内松开鼠标才会触发，但是必须加上dragover事件并且清除dragover事件的默认行为。
dragleave事件 在拖拽元素离开目标元素的时候触发，但是一旦我们阻止了dragover事件的默认事件，就不会再松开后触发一个dragleave事件。



11，由于HTML5中我们可以通过为表单元素添加multiple属性，因此我们通过<input>上传文件后得到的是一个FileList对象（伪数组形式）。

12，

if（navigator.userAgent.indexOf("Chrome") !== -1）{
	webkit
}else if（navigator.userAgent.indexOf("Firefox") !== -1）{
	moz
}

13,navigator.userAgent获取那个版本。

14，onchange事件 当调用者发生改变是触发。

15，FileReader对象
HTML5新增内建对象，可以读取本地文件内容。

var reader = new FileReader;

实例方法：
readAsDataURL()  以DataURL形式读取文件
事件监听：onload事件
reader.onload = function () {
				document.querySelector('img').src = this.result;
			}

16，百度地图api使用
1、获取当前地理信息
navigator. geolocation.getCurrentPosition(successCallback, errorCallback, options)
2、重复获取当前地理信息
navigator. geolocation.watchPosition(successCallback, errorCallback, options)

		 function success(position) {
		 	// alert(1);
		 	console.log(position);
		 }

		 // 失败的回调
		 function error(err) {
		 	console.log('error');

		 	console.log(err);
		 }

		 // 获得用户当前信息
		 navigator.geolocation.getCurrentPosition(success, error, {
		 	// enableHighAccuracy: true,
		 	// timeout: 3000,
		 	// maximumAge: 1000
		 });
position.coords.latitude纬度
position.coords.longitude经度
position.coords.accuracy精度
position.coords.altitude海拔高度

17,history.pushState({},'','地址');
			// 1、对象，在添加历史时，会设置一些数据，一般会设置null
			// 2、一般不生效，没意义
			// 3、我们要更改址址，并且会当一条新记录


   history.replaceState({key:123},'','地址');[这里添加的数据在后面onpopstate事件时可以读取和使用]
不会新生成网页记录,只是替换当前的地址.
			// 1、对象，在添加历史时，会设置一些数据，一般会设置null
			// 2、一般不生效，没意义
			// 3、我们要更改址址，并且会当一条新记录

   onpopstate()事件 在历史区发生改变后并操作历史区的时候.(历史发生改变后,在操作前进或后退会触发)
要绑定给window   window.onpopstate = function(state){}为了获取数据加载在页面中
以后当我们访问一个网站的时候发现地址发生了改变,网页局部发生了改变,实现网页更新,那么他就用了window.onpopstate事件实现的功能.(主要应用于单页面应用)


18，document.cookie  是一串字符串

19，sessionStorage 同窗口多页面
1，是存储在本地的浏览器窗口里，而不是存在地址中
2，只要是同一个浏览器窗口，跨页面以后也能得到
3，关闭浏览器窗口以后会自动删除
4，如果我们换一个浏览器窗口打开就没有了

20，localStorage
1，是存储在本地的浏览器中，不再是某一个窗口下，但是不能跨域（传输学医、域名、端口号只要有一个不一样）实现。
2，因为是存在浏览器的缓存中，所以关闭浏览器不会丢失数据
3，数据消失只能靠手动删除或者清除浏览器缓存

方法：
window.localStorage.getItem()
（sessionStorage/LocalStorage）：setItem("key","value")-->设置
（sessionStorage/LocalStorage）：getItem("key")-->获取，返回value值
（sessionStorage/LocalStorage）：removeItem（"key"）-->删除
（sessionStorage/LocalStorage）：clear()-->清空
（sessionStorage/LocalStorage）：key(0)-->按索引下标查找，返回的是"key"
window.localStorage.key(0);获取索引下标为0的值


21,应用缓存:
想用应用缓存第一步需要加载进来
在<html manifest="./study.appcache">
manifest文件格式
1、顶行写CACHE MANIFEST
2、CACHE: 换行指定我们需要缓存的静态资源，如.css、image、js等
3、NETWORK: 换行指定需要在线访问的资源，可使用通配符
4、FALLBACK: 换行当被缓存的文件找不到时的备用资源




CACHE MANIFEST

#版本号 1.0.0

CACHE:

#此部分写需要缓存的资源 如.css、image、js等

./images/img1.jpg
./images/img2.jpg
./images/img3.jpg
./images/img4.jpg
./images/img5.jpg

NETWORK: 

#此部分要写需要有网络才可访问的资源，无网络刚不访问(更新最新的内容来代替之前缓存的内容)    （记得清缓存）

#./js/main.js

*代表所有

FALLBACK:         回滚的意思

#当访问不到某个资源的情况下，自动由另一个资源替换

./css/online.css ./css/offline.css

./online.html ./offline.html
当我们找不到源文件就使用备用文件

应用缓存注意事项
1、CACHE: 可以省略，这种情况下将需要缓存的资源写在CACHE MANIFEST
2、可以指定多个CACHE: NETWORK: FALLBACK:，无顺序限制
3、#表示注释，只有当demo.appcache文件内容发生改变时或者手动清除缓存后，才会重新缓存。
4、chrome 可以通过chrome://appcache-internals/工具和离线（offline）模式来调试管理应用缓存
