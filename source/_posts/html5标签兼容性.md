---
title: html5兼容性
categories: ['前端']
tags: ['兼容性']
---
##HTML5的兼容性
- 因为在IE8及一下的IE版本是不兼容HTML5的新元素的，所以我们要是用HTML5开发的话，第一个要解决的就是兼容性的问题。
HTML5的兼容性

- 因为HTML5的新元素就是一些新的标签，IE只是不认识这些标签而已，那我们解决的问题就是让IE8一下版本的浏览器认识这些标签，或者说知道他就是一个标签，那么我们就解决了兼容性问题。
比如：header 这个标签在IE8及一下的版本的浏览器中是不认识的，但是我们却可以通过一小段JS代码来创建标签，通过JS来创建的标签浏览器是可以识别的，我们就可以利用这个点来解决兼容性问题。
这里就需要用到一个方法，document.createElement();


- `var oHeader = document.createElement("header");`//-> 动态创建一个标签‘header’
document.body.appendChild(oHeader)//-> 把header标签动态添加到body中
这样添加以后我们就可以在IE8下使用header标签了。但是，我们不确定我们的每一次开发中到底使用多少个header标签，也不确定具体要什么时候使用，如果说我们每一次使用的时候都写一小段JS代码来动态创建和动态添加的话，那就会很耗性能，所以我们只需要在最开始告诉浏览器一声，我创建了一个header标签就可以，至于什么时候用浏览器你就别管了，反正只要出现了这个标签你知道他是什么，会渲染他就可以了，我们就可以这样写


- `document.createElement("header");`
这样就可以了，以后你再使用header标签的时候，浏览器就会知道，他是一个标签，我就按照标签的标准来渲染他就行了。但是第二个问题出现了，那就是我们也不知道我会在这次开发中都使用到哪些个HTML5的标签，那么我们就把每一个HTML5标签都声明一遍就可以了。

- 这里就不用我们自己来写了，只需要引入一个JS文件就可以了。
就是 “html5shiv.min” 这个文件，里面已经帮我们把所有的都写好了，就不用我们每回自己写了。
这个时候出现了第三个问题，那就是我们引入了这个JS文件以后，那么不管这个浏览器是不是兼容HTML5标签，我们都声明了一遍，也就是说我们这一段JS代码都运行了，当然，这样做是没有问题的，可是这样对于已经可以兼容HTML5的浏览器来说就是浪费了，虽然这个文件很小，但是也会浪费一定的性能，作为一个开发人员来说，没一个KB的性能都是能省就省，尽量不出现一个多余的KB。所以，我们就只要让这个JS文件在IE8及以下版本的浏览器中运行就行了，这个时候我们就需要一种方法：

<!--[if lte IE 8]>
这个注释是只属于IE的，也就是说只有IE浏览器才认识	
<![endif]-->
这个注释的意思是，当浏览器是IE8及以下的版本的时候，才执行中间的代码。


- <!--[if lte IE 8]>
`<script>alert(123)</script>`
<![endif]-->
只有在IE8及一下版本的浏览器中，才会执行这个“alert(123)”这个命令，而其他的浏览器不会执行这一段代码。

所以我们可以用这个方法来引入刚才那段JS代码


- <!--[if lte IE 8]>
`<script src="./html5shiv.min"></script>`
<![endif]-->
这样就可以做到只在不兼容HTML5的浏览器中进行声明，而兼容的浏览器则直接跳过，这样做即解决了兼容性问题，也进行了性能优化。