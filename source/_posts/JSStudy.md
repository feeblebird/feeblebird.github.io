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

* 在事件处理程序中使用javascript

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
* JavaScript注释单行为//，注释多行为/\* \*/

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

# JavaScrip中函数的使用

* 函数的作用

  * 简化代码
  * 提高重用性
  * 减少工作量
  * 制作复杂代码

  ```html
  <html>
      <head>
          <title></title>
          <script type = "text/javascript">
          	function funcname()
              {
                  
              }
          </script>
      </head>
      <body>
          <div onmouseover = "funcname()";>
              
          </div>
      </body>
  </html>
  ```

# JavaScript中变量的使用

使用变量使得代码简洁且提高重用性。

```html
<!DOCTYPE html>
<html>
<head>
	<title>方块变化</title>
	<style>
		#ts{
			border-style : solid;
			border-width : 5px;
			border-color : blue;
			width : 200px;
			height : 200px;
		}
	</style>
	<script type = "text/javascript">
		function change1()
		{
			var oTs= document.getElementById("ts");
			oTs.style.width = "300px";
			oTs.style.height = "300px";
			oTs.style.border = "red 5px solid";
		}
		function change2()
		{
			var oTs= document.getElementById("ts");
			oTs.style.width = "200px";
			oTs.style.height ="200px";
			oTs.style.border = "blue 5px solid";
		}
	</script>
</head>
<body>
	<div id = "ts" onmouseover = "change1()"; onmouseout = "change2()";>
	</div>
</body>
</html>
```
> 也可以直接用id进行设置，但是上网查阅后由于兼容性问题和合法性问题，最好使用getElementById();
```html
<!DOCTYPE html>
<html>
<head>
	<title>方块变化</title>
	<style>
		#ts{
			border-style : solid;
			border-width : 5px;
			border-color : blue;
			width : 200px;
			height : 200px;
		}
	</style>
	<script type = "text/javascript">
		function change1()
		{
			//var oTs= document.getElementById("ts");
			ts.style.width = "300px";
			ts.style.height = "300px";
			ts.style.border = "red 5px solid";
		}
		function change2()
		{
			//var oTs= document.getElementById("ts");
			ts.style.width = "200px";
			ts.style.height ="200px";
			ts.style.border = "blue 5px solid";
		}
	</script>
</head>
<body>
	<div id = "ts" onmouseover = "change1()"; onmouseout = "change2()";>
	</div>
</body>
</html>
```

> js作业，方块变化

```html
<!DOCTYPE html>
<html>
<head>
	<title>方块变化</title>
	<style>
		#ts{
			background : #0cfeda;
			width : 200px;
			height : 200px;
		}
	</style>
	<script type = "text/javascript">
		function change1()
		{
			var oTs= document.getElementById("ts");
			oTs.style.width = "300px";
			oTs.style.height = "300px";
			oTs.style.background = "#00ff00";
		}
		function change2()
		{
			var oTs= document.getElementById("ts");
			oTs.style.width = "200px";
			oTs.style.height ="200px";
			oTs.style.background = "#0cfeda";
		}
	</script>
</head>
<body>
	<div id = "ts" onmouseover = "change1()"; onmouseout = "change2()";>
	</div>
</body>
</html>
```



# 我们可以利用JavaScript改变html文件中的任何一个元素

# 利用JS实现日间夜间模式的切换

```html
<!DOCTYPE html>
<html>
<head>
    <title>方块变化</title>
	<link id = "lk" rel="stylesheet" type="text/css" href="day.css">
	<script type = "text/javascript">
		function night()
		{
			document.getElementById("lk").href = "night.css"
		}
	</script>
</head>
<body>
	<p>
		aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa<br />aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa<br />aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa<br />aaaaaaaaaaaaaaaaaaa
	</p>
	<a href = "javascript:" onclick = "night()";>夜间模式</a>
	<a href = "javascript:">日间模式</a>
</body>
</html>
```

```css
/*day.css*/
*{
    font-size : 14px;
    color : #000000; /*字体颜色*/
    background : #ffffff;
}
```

```css
/*night.css*/
*{
    font-size : 20px;
    color : #ffffff;
    background : #000000;
}
```

# 变量命名法(匈牙利命名法)

![](https://i.loli.net/2020/09/21/Zi1lQBIXH6URx4t.png)

# JavaScript的数据类型

![](https://i.loli.net/2020/09/21/rCa7UzY9ZRPolvT.png)

> JS的基本类型属于弱类型，在声明时并不确定它是什么类型，是根据赋值的具体情况来确定的，所以它存储的是什么类型的值，他就是什么类型的变量。

* #### typeof运算符

  我们可以利用typeof运算符获取变量的数据类型，typeof(var);

* #### 类型转换

  * 强制类型转换

  * parseInt() //I大写
  * parseFloat()
  * 隐式类型转换
  * ==
  * 减法

```html
<!--实现加法-->
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script>
		function compute()
		{
			var one = document.getElementById("first");
			var two = document.getElementById("second");
			var ans = document.getElementById("result");
			var oneint = parseInt(one.value);
			var twoint = parseInt(two.value);
            if(isNaN(oneint)||isNaN(twoint))
                {
                    alert("输入有误");
                }else
                    
			ans.value = oneint + twoint;
		}
	</script>
</head>
<body>
	<input id = "first" type = "text" />
	+
	<input id = "second" type = "text" />
	<input type = "button" value = "=" onclick = "compute()"; />
	<input id = "result" type = "text" />
</body>
</html>
```

* isNaN()函数判断是否为数字，用来规范用户输入

# JavaScript中使用for语句

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script type = "text/javascript">
		var j = 0;
		var i;
		for(i = 1; i <= 100;i ++)
		{
			if(i%2==0)
			{
				j = j+i;
			}
		}
		document.write(j);
	</script>
</head>
<body>

</body>
</html>
```

# JavaScript中Date()对象及Array使用

* #### Date()对象定义

  ```html
  var d = new Date();
  ```

* #### Date()对象方法

  ![](https://i.loli.net/2020/09/21/DuX8aSdtvjriVJG.png)

  ![](https://i.loli.net/2020/09/21/2zje4NRcyadB7wi.png)  

  ![](https://i.loli.net/2020/09/21/xYEpsTnc2jwK8hF.png)

  ![](https://i.loli.net/2020/09/21/lDcy3d2SiIGj6J7.png)

* #### Array()定义及使用

  * 数组用于存储具有相同数据类型的一组值，使用下标来区分各个值。
  * 在JavaScript中，数组的下标以开始。
  * JavaScript没有明确的数组数据类型，但却有内置的数组对象。要在程序中使用数组，必须使用数组对象及其相关联的方法。

  ```html
  var name = new Array([element0,element1,...,elementn]);
  ```

* #### 数组的初始化

  * 将指定的值作为其元素
  * 使用arrayName = new Array(N); 指定元素个数

  同一个数组中不同元素的类型可以不同。

* #### 数组的length属性

  ```html
  <script type = "text/javascript">
  	var a = new Array("first","second","third");
      a[48] = "12";
      document.write(a.length);
      //显示的结果是49
  </script>
  ```

* #### 数组的遍历

  ```html
  var a = new Array("first","second","third");
  for(var i = 0;i < a.length; i++)
  {
  	                    
  }
  //for 循环
  ```

  ```html
  var arr = new Array("fist","second","third");
  for(var item in arr)
  {
  	document.write(arr[item]+',');
  }
  ```

* #### 数组添加删除元素

  * 添加
    * push()，从尾部添加
    * unshift()，从头部添加
  * 删除
    * pop()，从尾部弹出
    * shift()，从头部弹出

# 利用Date()对象和InnerHTML()和setTimeout()实现动态时间显示

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<script type="text/javascript">
		function showtime()
		{
			var week = new Array("周日","周一","周二","周三","周四","周五","周六");
			var d = new Date();
			var ye = d.getYear();
			var mo = d.getMonth();
			var da = d.getDate();
			var ho = d.getHours();
			var mi = d.getMinutes();
			var we = d.getDay();
			var se = d.getSeconds();
			var now = "现在是"+(ye+1900)+"年"+(mo+1)+"月"+da+"号"+"<br />";
			if(ho<12)
			{
			 	now = now +"早上";
			}else if(ho>=12&&ho<18)
			{
				now = now +"下午";
			}else
			{
				now = now +"晚上";
			}
			now = now + +ho+"时"+mi+"分"+se+"秒"+"<br />"+week[we];
			var t = document.getElementById("time");
			t.innerHTML = now;
			setTimeout("showtime()",1000);
		}
	</script>
</head>
	<body id = "time" onload = "showtime()";>
	</body>
</html>  
```

* #### setTimeout("funcname",ms)

  每隔多少毫秒执行那个函数，可在函数内递归调用

* #### innerHTML属性

  * innerHTML属性可以设置或者返回指定元素的HTML内容
  * 语法结构一

  ```javascript
  htmlContent = domObj.innerHTML;
  //获取指定元素内的HTML内容
  ```
  * 语法结构二
  
  ```javascript
  domObj.innerHTML = htmlContent
  //为指定元素设置HTML内容
  ```
  
  * 代码实例
  
  ```html
  <!doctype html>
  <html>
  <head>
  <meta charset="utf-8">
  <meta name="author" content="http://www.softwhy.com/" />
  <title>蚂蚁部落</title>
  <script type="text/javascript"> 
  window.onload=function(){
    let odiv = document.getElementById("ant");
    odiv.innerHTML = "蚂蚁部落";
  }
  </script>
  </head>
  <body>
  <div id="ant"></div>
  </body>
  </html>
  ```
  
  > 运行效果即为在id位ant的div中加了"蚂蚁部落"这句话
  >
  > **特别说明**：innerHTML属性是重置元素HTML内容，而不是追加
  
  ```html
  <!doctype html>
  <html>
  <head>
  <meta charset="utf-8">
  <title>蚂蚁部落</title>
  <script type="text/javascript"> 
  window.onload=function(){
    let odiv = document.getElementById("ant");
    odiv.innerHTML="蚂蚁部落";
  }
  </script>
  </head>
  <body>
  <div id="ant">青岛市南区</div>
  </body>
  </html>
  ```
  
  > 青岛市南区被蚂蚁部落覆盖了
  
  ```html
  <!doctype html>
  <html>
  <head>
  <meta charset="utf-8">
  <meta name="author" content="http://www.softwhy.com/" />
  <title>蚂蚁部落</title>
  <script type="text/javascript"> 
  window.onload=function(){
    let odiv = document.getElementById("ant");
    odiv.innerHTML = "<b>蚂蚁部落</b>";
  }
  </script>
  </head>
  <body>
  <div id="ant"></div>
  </body>
  </html>
  ```
  
  > 显示的是加粗的蚂蚁部落，所以赋值给innerHTML的字符串都会被当作HTML代码解析
  
  innerText属性可以返回指定元素内的文本内容
  
  ```html
  <!doctype html>
  <html>
  <head>
  <meta charset="utf-8">
  <meta name="author" content="http://www.softwhy.com/" />
  <title>蚂蚁部落</title>
  <script type="text/javascript"> 
  window.onload=function(){
    let odiv = document.getElementById("ant");
    alert(odiv.innerText);
  }
  </script>
  </head>
  <body>
  <div id="ant"><b>蚂蚁部落</b></div>
  </body>
  </html>
  ```
  
  > 返回的是蚂蚁部落，而没有包括html标签

# 使用javascript实现一个算数计算器

* #### 网上代码(自己还没改完善)

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type = "text/css">
		#main{
			width : 400px;
			height : 500px;
			background-color : #f2f2f2;
			border : 1px solid #c2c3c6; /*边框为实线*/
			margin : auto; /*外边距自动设置*/
		}
		#window{
			height : 70px;
			width : 335px;
			background-color : #323232;
			border : 1px double #ffffff;  /*边框为双边框，厚度为1像素，颜色为白色*/
			margin : 25px 25px 25px 25px; /*top right bottom left外边距*/
			font : 40px "微软雅黑";
			color : #ffffff; /*字体颜色为白色*/
			padding-right : 10px;
		}
		#func{
			padding: 0 20px;
			position : relative;/*设置定位方式为相对定位*/
		}
		#func input{ /*设置#func中的input样式*/
			height : 40px;
			width :60px;
			margin : 10px 10px;
			/*font : ;*/
		}
		#add,#sub,#mul,#div,#equal,#dele{
			position : absolute;
			right : 30px;
		}
		#point,#three,#six,#nine{
			position : absolute;
			right : 120px;
		}
		#zero2,#two,#five,#eight{
			position : absolute;
			right : 210px;
		}
		#zero,#one,#four,#seven,#res{
			position : absolute;
			right : 300px;
		}
		#add,#res{
			top : 60px;
		}
		#sub,#nine,#eight,#seven{
			top : 120px;
		}
		#mul,#six,#five,#four{
			top : 180px;
		}
		#div,#three,#two,#one{
			top : 240px;
		}
		#equal,#point,#zero2,#zero{
			top : 300px;
		}
	</style>
	<script type = "text/javascript">
		window.onload = function(){

            // 数据容器
            var left = 0;   //被除数
            var right = 0;  //除数
            var sum = 0;    //和  

            var numb = 0;   //此变量用来限制点的输入     
            // 获取id并返回
            function get(id){
                return document.getElementById(id);
            }
            // 运算函数
             function operation(id){            
                if( get("window").value != "0"){
                    if(left == 0)
                    {
                        get("window").value = get("window").value + get(id).value;
                        left = parseFloat(get("window").value);
                    }
                }

                //numb 转为number类型 让点可以再输入一次
                numb = 0;
            }

            // 数字盘函数
            function figure(id){ 
            
                // 判断被除数是否有值
                if(left == 0)
                {
                    // 改变value默认值
                    if (get("window").value === "0" ) {
                        get("window").value = get(id).value; 
                    }else{
                        get("window").value = get("window").value + get(id).value;    
                    }                                
                }else{
                    get("window").value = get("window").value + get(id).value;
                    var str = get("window").value;
                    var num = "";                    
                    // 获取第二次输入的数字
                    for (var i = 0; i < str.length; i++) {
                        // 判断加减乘除
                        if(str[i]== "+"){
                            for (var j = i + 1; j < str.length; j++) {
                                num+=str[j];
                                
                            };
                            right = parseFloat(num);
                        }else if(str[i]== "-"){
                            for (var j = i + 1; j < str.length; j++) {
                                num+=str[j];
                                
                            };
                            right = parseFloat(num);
                        }
                        else if(str[i]== "*"){
                            for (var j = i + 1; j < str.length; j++) {
                                num+=str[j];
                                
                            };
                            right = parseFloat(num);
                        }
                        else if(str[i]== "/"){
                            for (var j = i + 1; j < str.length; j++) {
                                num+=str[j];
                                
                            };
                            right = parseFloat(num);
                        }
                    };                    
                }

                // 清空所有数据  
                if(sum != 0){
                    left = 0;
                    right = 0;
                    sum = 0;
                    numb = 0;
                    get("window").value = get(id).value;
                }
            
            }


　　　　　　　// 数字键盘区----------------------------------------------------------开始
            get("one").onclick = function(){ 
                figure("one");
            }
            get("two").onclick = function(){ 
                figure("two");
            }
            get("three").onclick = function(){ 
                figure("three");
            }
            get("four").onclick = function(){ 
                figure("four");
            }
            get("five").onclick = function(){ 
                figure("five");
            }
            get("six").onclick = function(){ 
                figure("six");
            }
            get("seven").onclick = function(){ 
                figure("seven");
            }
            get("eight").onclick = function(){ 
                figure("eight");
            }
            get("nine").onclick = function(){ 
                figure("nine");
            }
            get("zero").onclick = function(){ 
                figure("zero");
            }
 
　　　　　　  // 数字键盘区----------------------------------------------------------结束
            



　　　　　　　//功能区-----------------------------------------------------------开始

            // 加
            get("add").onclick = function(){             
                operation("add");
            }


            //减
            get("sub").onclick = function(){             
                operation("sub");
            }

            // 乘
            get("mul").onclick = function(){
                operation("mul");
            }
            
            // 除
            get("div").onclick = function(){
                operation("div");
            }

            // 点
            get("point").onclick = function(){
                // 限制点的输入
                if(numb === 0 && sum == 0){ //numb值等于0 类型等于number                        
                    get("window").value = get("window").value + get("point").value;
                    numb = (get("window").value); //numb赋值为字符串
                }

            }

            // 清除
            get("res").onclick = function(){
                if(get("window").value != "0")
                {                        
                    left = 0;
                    right = 0;
                    sum = 0;
                    numb = 0;
                    get("window").value = "0";
                }
            }

            // 求和
            get("equal").onclick = function(){  
                var symbol = "";           
                if(left != 0 && right != 0){
                    for (var i = 0; i < get("window").value.length; i ++ ) {
                        symbol = get("window").value[i];
                        if(symbol == "+"){
                            sum = left + right;
                            get("window").value = sum;
                        }else if(symbol == "-"){
                            sum = left - right;
                            get("window").value = sum;
                        }
                        else if(symbol == "*"){
                            sum = left * right;
                            get("window").value = sum;

                        }
                        else if(symbol == "/"){
                            sum = left / right;
                            get("window").value = sum;
                        }
                    };
                }                            
            }
            
        }

	</script>
</head>
<body>
	<div id = "main">
			<input type = "text" id = "window" disabled="disabled" style = "text-align : right" value = "0" />
			<div id = "func">
				<input type = "reset" id = "res" value = "C"  />
				<input type = "button" id = "add" value = "+" />
				<input type = "button" id = "sub" value = "-" />
				<input type = "button" id = "mul" value = "*" />
				<input type = "button" id = "div" value = "/" />
				<input type = "button" id = "point" value = "." />
				<input type = "button" id = "equal" value = "=" />
				<input type = "button" id = "zero" value = "0" />
				<input type = "button" id = "zero2" value = "00" />
				<input type = "button" id = "dele" value = "del" />
				<div id = "numb">
					<input type = "button" id = "one" value = "1" />
					<input type = "button" id = "two" value = "2" />
					<input type = "button" id = "three" value = "3" />
					<input type = "button" id = "four" value = "4" />
					<input type = "button" id = "five" value = "5" />
					<input type = "button" id = "six" value = "6" />
					<input type = "button" id = "seven" value = "7" />
					<input type = "button" id = "eight" value = "8" />
					<input type = "button" id = "nine" value = "9" />
				</div>
			</div>
	</div>
</body>
</html>
```

* #### 简易实现代码

```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<form>
		<input type = "text" />
		<select>
			<option >+</option>
			<option>-</option>
			<option>*</option>
			<option>/</option>
		</select>
		<input type = "text" />
		<input type = "button" value = "=" />
		<input type = "text" />
	</form>
</body>
</html>
```

