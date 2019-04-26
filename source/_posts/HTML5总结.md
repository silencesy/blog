---
title: html5基础
categories: ['前端']
tags: ['html5']
---
1. HTML5的语法规范
   html:4s/4t/xs/xt/5     !
2. 语义化
   --标签  header  footer  nav  section   article  aside  progress  video  audio
   --输入类型  email  url  tel  num  search  range  color  time  date  dateTime  week  month
   --表单元素  output  meter  keygen dataList
   --表单属性  placeholder  autofocus  multiple  autocomplete  novalidate  required  form  pattern
3. 多媒体
   --audio loop autoplay  controls
   --video loop autoplay  controls  width  height
4. DOM扩展
   --获取元素  document.getElementsByClassName()  querySelector()  querySelectorAll()
   --类名操作  classList.add()  classList.remove()  classList.toggle()  classList.contains()
   --自定义属性  dataset[key]='value'  dataset[key]   前缀名“data-*”
5. H5API
   --online()/offline()  和“onLine”属性  在线状态/离线状态   检测是否在线
   --fullScreen  webkitIsFullScreen检测是否全屏  requestFullScreen（）开启全屏  cancelFulScreen()关闭全屏  注意加前缀（webkit-谷歌，moz-火狐） 关闭全部用document调用  document全屏时写成document.documentElement.requestFullScreen
   --fileReader  获取的图片信息  ele.files[0]  new FileReader()  reader.readAsDataURL(图片信息)  src赋值
   --drag  拖拽元素draggable="true" 默认不可以被拖拽的元素加上这个属性以后就可以被拖拽
       -- dragstart  拖拽开始
       -- dragend  拖拽结束
       -- dragleave  光标离开拖拽元素
       -- drag  拖拽过程中
           目标元素  页面上任意一个元素都可以是拖拽元素，不用特殊设定
       -- dragenter  拖拽元素进入目标元素时
       -- dragover  拖拽元素在目标元素内
       -- dragleave  拖拽元素离开目标元素
       -- drop  拖拽元素在目标元素内松开鼠标
6. 地理定位
   -- geolocation.getCurrentPosition(successCallback, errorCallback, options)
   -- geolocation.watchPosition(successCallback, errorCallback, options)
   -- 成功回调是我们能得到一个position
        position.coords.latitude纬度
        position.coords.longitude经度
        position.coords.accuracy精度
        position.coords.altitude海拔高度
   -- 失败回调我们能得到一个error  里面写的是错误信息
   -- 使用百度的API接口
7. history
   -- history.pushState(null,'','地址')
   -- history.replaceState(null,'','地址')
   -- onpopstate()事件  在历史区发生改变后并且操作历史区的时候
8. web存储
   -- sessionStorage  同窗口多页面保存数据  关闭窗口后删除
   -- localStorage  多窗口保存页面  不会自动删除，只能手动删除
       setItem("key","value")  增加或更改
       getItem("key")  获取
       removeItem("key")  删除
       clear()  清空
       key(0)  按照下标回去，返回的是“key”
9. 应用缓存，配置静态资源文件
   CACHE MANIFEST

   # 版本号

   CACHE:

   需要缓存的资源

   NETWORK:

   当网络重新连接时需要重新获取的资源

   FALLBACK:

   （源文件）\s（备用文件）
   当我们找不到源文件的时候启用备用文件

10,jquery视频编写
1,oncanplay()检测视频可以播放时触发
2,video.duration获取视频的总时长
3,video.paused判断视频播放还是暂停
4,toggleClass切换按钮状态
5,video.currentTime获取当前的播放进度

11,分隔字符串返回数组方法为  str.split("分隔符")  分隔符为: , 等.