---
title: html5表单
categories: ['前端']
tags: ['html']
---
## HTML5的表单
- HTML5的第二个大特点就是他的各种表单控件，也是非常强大的功能。
- 输入类型

+ 输入类型，顾名思义就是我们在写input标签时type后面的属性值，我们以前接触的有

		<input type="text">//-> 文本框
		<input type="password">//-> 密码框
		<input type="checkbox">//-> 复选框
		<input type="radio">//-> 单选框
		<input type="submit">//-> 提交
		<input type="button">//-> 按钮
		<input type="reset">//-> 重置
		<input type="file">//-> 文件选择
+ 这些都是我们以前的输入类型，但是对于今天的开发，这些类型已经不够用了，我们需要更多更细致的分类

		<input type="email">//-> email地址匹配
		<input type="url">//-> url地址匹配
		<input type="tel">//-> 电话号码
		<input type="number">//-> 数字
		<input type="search">//-> 搜索框
		<input type="color">//-> 拾色器
		<input type="time">//-> 时间选择
		<input type="date">//-> 日期选择
		<input type="month">//-> 月份选择
		<input type="week">//-> 周选择
- 这些新加入的输入类型，大大的降低了我们的代码量。比如，email框，以前我们要是想让这个框里输入的一定是email地址的话，我们需要用JS获取这个input框的value，然后写一段正则来匹配，最后在返回结果。而现在我们只需要在HTML中写个email类型的input框就可以了。

- 当然了，这里面有一些是针对移动设备的，并且有兼容性问题，所以我们在开发过程中一定要根据需求选择性的来使用。
## 表单元素

- 表单元素其实就是HTML5中新增加的一些属于表单的新标签。
- 以前我们接触的表单元素有

		<form></form>//-> 表单
		<fieldset></fieldset>//-> 表单框
		<legend></legend>//-> 表单框的标题
		<label></label>//-> 表单里的控件标签
		<textarea></textarea>//-> 文本区域
		<select></select>//-> 选择列表
		<option></option>//-> 选择列表的下拉项


##### 下面是我们HTML5中新增加的表单元素
		<datalist></datalist>//-> 数据列表
		<output></output>//-> 输出结果
		<meter></meter>//-> 度量器
		<keygen></keygen>//-> 生成加密字符串
- 这些都是为了我们的开发效率更快而诞生的，大家只需要记住就好。

#### 表单属性

- 表单属性就是对于一些表单元素的修饰，因为光靠现在的表单输入类型加上现有的表单元素，还是不能满足我们的各式各样的需求，所以就需要在依靠表单属性来帮我们做一些小细节的处理。
- 比如：我们要一个文本框只能输入数字，以前只能靠一小段JS代码来实现，现在可以直接用“input type=”number””就可以了，但是如果我只想让他输入10到20之间的数字的时候，就必须要表单属性来帮助了。


		<input type="number" min="10" max="20">
- 这样的话就只能填写10到20之间的数字了。

- 以前我们还接触过很多表单属性，比如value等，我们就不意义列举了，直接介绍一下HTML5新增的属性

		placeholder//-> 占位符
		autofocus//-> 自动获取焦点
		multiple//-> 多文件上传
		autocomplete//-> 自动填充
		form//-> 表单关联
		novalidate//-> 关闭验证
		required//-> 必填
		pattern//-> 自定义验证
- 通过这些表单属性，我们可以在HTML页面更加细致的处理一些表单的细节，而不需要借助JS。做到了节约性能。