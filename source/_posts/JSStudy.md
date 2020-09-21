---
title: JSStudy
date: 2020-09-20 19:56:52
tags: JS
categories: JS
---

# 什么是JavaScript Script(脚本)

* JavaScript是一种基于对象的解释型脚本语言
* 可用于创建客户端脚本和服务器端脚本

* 核心: ECMAScriptS

  文档对象模型:DOM Document Object Model

  浏览器对象模型:BOM Browser Object Model

# JavaScript使用方式

* 使用独立的JavaScrip解释器

* 使用浏览器内核中内嵌的JavaScript解释器

  * 直接在console中输入脚本并执行

  * 将js代码内嵌到html文件中
```javascript
<script type = "text/javascript">    
	window.alert("hello!");
</script>
```

# 将JS代码嵌入到html文件中

* html文件中内嵌\<script\>...\</script>

```html
<html>
	<head>
		<script language = "JavaScript">
			<!--对较早浏览器隐藏脚本
				document.write("欢迎使用JavaScript");
			//脚本隐藏结束
			-->
		</script>
	</head>
	<body>
		<p>祝学有所成</p>
	</body>
</html>
```

* 外部导入\<script src = "xxx.js"\>/</script\>

  html文件中

```html
<html>
    <head>
        <script src = "xxx.js"></script>
    </head>
    <body>
        <P>
            祝学有所成!
        </P>
    </body>
</html>
```

  	js文件中

```javascript
document.write("嗨！你好吗？")
```

* 在时间处理程序中使用javascript

```html
<html>
    <head>
        <title>JavaScript示例</title>
    </head>
    <body>
        <form>
            <input type = "button" value = "你好"
                   onClick = 'alert("你好!!");'> <!--这里是单引号,单双引号作用都一样，只是为了区分，所以也可以写成onClick = "alert('你好!!');"-->
        </form>
    </body>
</html>
```

# 写出的代码利用浏览器解释器进行检查

* 写出的代码不能正确执行，可以在浏览器检查的console中查看错误信息。

# 常用事件

* #### onclick

* #### onmouseover、onmouseout

* #### onload

# 使用Alert/Confirm/Write方法

* 使用窗口的Alert方法，可以生成一个对话框
* 使用窗口的Confirm方法，可以生成一个确认对话框
* 使用document的Write方法可以创建页面内容

```html
<html>
    <head>
        <script language = "JavaScript">
        	<!--
            	alert("确定");//window.alert("确定");
            	document.write("谢谢!");
            	if(confirm("是否要关闭当前窗口?")){window.close();}
            -->
        </script>
    </head>
</html>
```

# 注意事项

* 区分大小写
* 每句语句以分号结尾
* JavaScript注释单行为//，注释多行为/* */

# 样例1

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type = "text/css">
		#ts{
			width : 200px;
			background : #ff9900;
			color : #ffffff;
			font-size : 12px;
			padding : 5px;
			display : none;
			//display决定对象的显示方式block显示,none隐藏
		}
		#example{
			width : 450px;
			background : #ff9900;
			font-size : 18px;
			line-height : 28p;
		}
	</style>
</head>
<body>
	<div id = "example">
		例1：鼠标移入显示提示文本框<br />
		1.实现网页布局<br />
		2.给对象设计样式，把对象的display样式为none<br />
		3.使用js来操纵样式<br />
		当鼠标移入的时候onmouseover,使对象显示<br />
		更改对象的display样式为block<br />
		ts.style.display = "block";<br />
		当鼠标移出的时候onmouseout,使对象隐藏<br />
		更改对象的display样式为none<br />
		ts.style.display = "none";<br />
	</div>
	<form>
		username:<input type = "text" />
		<br />
		password:<input type = "password" />
		<br />
		<input type = "checkbox" onmouseover = "ts.style.display = 'block'"; onmouseout = "ts.style.display = 'none'";>记住我的登录信息
		<br />
		<div id = "ts">
			如果是公用电脑，请勿选择此选项
		</div>
		<br />
		<input type = "button" value = "上交" />
		<input type = "reset" value = "重来" onclick = "window.confirm('你的输入将被清空')" />
	</form>
</body>
</html>
```

> html设计结构
>
> css控制表现
>
> js控制行动