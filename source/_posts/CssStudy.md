---
title: CssStudy
date: 2020-09-14 08:11:19
tags: css
categories: Web前端第三个第四个
---

# CSS上课实例

```css
<!DOCTYPE html>
<html>
<head>
	<meta charset = "utf-8">
	<title>css学习</title>
	<style type = "text/css">
		a:link{color :#ff0000;text-decoration :none;}
		a:visited{color : #00ff00;}
		a:hover {color : #ff00ff; font-size : 140px;text-decoration : underline;}
		<!--hover要放在link，visited后面-->
		a:active {color : #0000ff;}
		.zuoye{
			font-size : 12pt;
			color : green;
			text-align : center;
			font-weight : bold;
			background-color : black;
		}
		h2,h3,h4,h5,h6{
			color : white;
			background-color : blue;
		}
		#left{
			color : black;
			background-color : green;
			font-size : 30px;
		}
		.red{
			color : red;
		}
	</style>
</head>
<body>
	<h1 style = "color : white;background-color : black;">我的css页面</h1>
	<h1 ><a target = "_blank" href = "http://www.runoob.com">我的css页面</a></h1>
	<div>哈哈哈哈</div>
	<div>hehhehehehe</div>
</body>
</html>
```

# Css(Cascading Style Sheet)作用

Cascading Style Sheet 层叠样式表，是用于控制网页样式并允许将样式信息与网页内容分离的一种标记性语言。Css是用来美化html实现的结构的

# Css特点

* CSS使页面载入更快
* CSS可以降低网站的流量费用
* CSS使设计师在修改设计时更有效率，而代价更低
* CSS使整个站点保持视觉的一致性
* CSS使站点可以更好地被搜索引擎找到
* CSS使站点对浏览者和浏览器更具亲和力

# 参考手册

[这里](https://www.w3school.com.cn)

# 基本语法

css语法有三个部分组成：选择符、属性、属性值

> 属性和属性值要用花括号包起来

```css
selector{
    property : value;
}
```

* selector 选择器通常是您需要改变样式的html元素。
* 每条声明由一个属性(property)和一个属性值(vlaue)组成。
* 属性(property)是希望设置的央视属性(style attribute)。每个属性有一个属性值(value).
* 属性和属性值被冒号分开。
* 后面以分号结束。
* 花括号里面都是以小写去写。

# css中的注释

不管是单行还是多行都是/\* \*/

# 引用方式

css引用方式：行间样式、内部样式、外部样式、导入外部样式。

* #### 行间样式：直接在标签上书写样式

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf-8"/>
  	<title>css引用方式</title>
  </head>
  <body>
  	<!--行间样式-->
  	<div style="color:olive;width:100px;border:1px solid blue;">行间样式测试1</div>
  	<div>行间样式测试2</div>
  	<!--内部样式-->
  </body>
  </html>
  ```

* #### 内部样式：写在head标签中

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf-8"/>
  	<title>css引用方式</title>
  	<!--2.内部样式-->
  	<style> 或者 <style type = "text/css">
  		p{
  			background-color: #eeeeee;
  			font-size: 18px;
  			font-style: italic;
  		}
  	</style>
  </head>
  <body>
  	<p>段落1</p>
  	<p>段落2</p>
  </body>
  </html>
  ```

* #### 外部样式：将其独立出来成一个文件，用link标签引入

  * 新建一个stylesheeat文件，扩展名为css
  * 在head标签中用link **(单标签)** 标签将css文件引入html中
  * link标签最好放到style标签之前
  
* html文件中
  
  ```html
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf-8"/>
  	<title>css导入方式</title>
  	<link rel = "stylesheet" type = "text/css" href = "test.css">
  </head>
  <body>
  	<span>外部导入样式测试</span>
  	<span>外部导入样式测试</span>
  	<span>外部导入样式测试</span>
  </body>
  </html>
  ```
  * css文件中
  
  ```css
  span{
      font-size : 15px;
      color : red;
      display : block;
  }
  ```
  
* #### 导入外部样式：独立出一个css文件，用import标签导入

  * 先创建一个css文件
  * 在style标签中，用import标签导入css文件
  * html文件中

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf-8"/>
  	<title>导入外部样式</title>
      <style>
      	@import "test.css"
      </style>
  </head>
  <body>
  	<div class = "box">导入外部样式</div>
  	<div class = "box">导入外部样式</div>
  	<div class = "box">导入外部样式</div>
  	<em class = "box">通四点零分</em>
  </body>
  </html>
  ```

  * css文件中

  ```css
  .box{
  	font-weight : bold;
  	font-size : 16px;
  	color : red;
  }
  ```

* #### 四种引用方式的区别

  * 行间样式只作用于当前标签，而内部样式作用于当前文件，外部样式可以被多个html文件引用。
  * 最好使用外部样式，实现结构

* #### link和import区别

  * link是XHTML标签，除了加载CSS外，还可以定义RSS等其他食物；@import属于CSS范畴，只能加载CSS。
  * link引入CSS是，在页面载入的同时加载；@import需要页面网页完全载入后加载。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       
  * link是XHTML标签，无兼容问题；@import是在CSS2.1上提出的，低版本的浏览器不支持。
  * link支持使用Javascript控制DOM去改变样式；而@import不支持。
  
* #### 如果样式发生冲突

  则优先级为: **行内样式** > **内嵌样式** > **外部样式表**

# 选择符

* 选择符通常是 **通配选择符**、**标记选择符**、**包含选择符**、**ID选择符**、**类选择符** 和 **选择符分组**。

* #### 通配选择符

  通配选择符的写法是"*"，其含义是所有元素。但一般性能不好

* #### 标记选择符

  标记选择符即使用HTML中元素名称作为选择符，如body，p，div等。

  每一种html标记的名称都可以作为相应的标记选择器的名称。

* #### 包含选择符

  包含选择符的结果是同时选中各个基本选择符所选择的范围。任何形式的选择符（包括标记、class、id、选择符等等）都可以作为包含选择符的一部分。

  **通过依据元素在其位置的上下问关系来定义样式**

  ```css
  li strong{
      font-stylle : italic;
      font-weight : normal;
  }
  ```

  ```html
  <li><strong>我是斜体字，因为strong元素位于li元素内</strong></li>
  ```

* #### ID选择符

  写法如下：#name(名称唯一)

  说明：ID选择符的语法格式是"#"加上自定义的ID名称。

  ```html
  #name{
  	font-size : 12px;
  }
  ```

  * id选择器的使用方法与class选择器基本相同，不同指出在于 **id选择器只能在HTML页面中使用一次**，针对性更强。
  
* #### ID选择器与包含选择器

  在现代布局中，id选择器常常用于建立 **包含选择器**

  ```css
  #sidebar p{
      font-style : italic;
      text-align : right;
      margin-top : 0.5em;
  }
  //id="sidebar"的元素中的p标签的样式是这样设置的
  ```

* #### 类选择符

  写法如下：.name

  类选择符的语法格式是"."加上自定义的类名称。

  ```css
  .name{
      font-size : 12px;
  }
  //所有调用类名为name页面元素中，文本的字体大小为12个像素。名称不唯一，可通过定义相同的类名来调用同一个样式。
  ```

  ```html
  .center{
  	text-align : center;
  }
  <h1 class = "center">
      this heading will be center-aligned
  </h1>
  <p class = "center">
      this paragraph will also be center-aligned
  </p>
  ```

  * 类选择器与id选择器一样，class也可被用作 **包含选择器** 

  ```css
  .fancy td{
      color : #f60;
      background : #666;
  }
  //调用了这个类的元素中的td标签的样式为这样设置的
  ```

* #### 选择符分组

  当多个选择符应用相同的样式，可以将选择符用英文逗号分隔的方式，合并为一组。

  ```css
  p,div,td{
      text-align : center;
  }
  ```

* #### 伪类和伪元素

  伪类和伪元素也是一种选择符，在页面元素中，用来定义超出结构所能标识的样式。伪类是能被支持CSS的浏览器自动识别的特殊选择符。

  ```css
  //语法结构如下:
  //选择符:伪类{属性:属性值;}
  //例: a:hover{font-size : 12px;}
  //说明:当鼠标讲过带有链接的文本上时，文本字体大小12像素。
  //伪类和伪元素的写法，一般以:开头，与类不同的是，伪类和伪元素在CSS中是指定的，不能随意的命名和定义。
  ```

* #### 伪类选择器

  ```css
  //锚伪类-链接的不同状态:未被访问状态、已被访问状态、鼠标悬停状态、活动状态
  a:link{color : #ff0000;} /*unvisited link*/
  a:visited{color : #00ff00;} /*visited link*/
  a:hover{color : #ff00ff;} /*mouse over link hover盘旋、靠近*/
  a:active{color : #0000ff;} /*selected link*/
  ```

  > 1.在css定义中，a:hover必须被置于a:link 和 a:visited之后，才是有效的
  >
  > 2.在css定义中，a:active 必须被置于a:hover 之后，才是有效的
  >
  > 3.伪类名称对大小写不敏感

* #### CSS属性

  ​        常用的属性有:字体属性、文本属性、背景属性、定位属性、尺寸属性、布局属性、边界属性、边框属性、补白属性、列表项目属性、表格属性。

  ​		其中，某些属性只有部分浏览器支持，这使得属性的应用变得相当的复杂，属性的知识和应用，是css的应用主体部分。

* #### CSS代码书写规范

  * 基本书写规范

    建议先书写类型选择符和重复使用的样式，然后是伪类，最后是自定义的选择符。除了重复使用的选择符，其它选择符按照使用的先后书写，这样便于修改时查找。

  * 命名参考

    ![](https://i.loli.net/2020/09/21/UFCDAxgoKjvzTtc.png)

  * 样式表书写顺序

    ![](https://i.loli.net/2020/09/21/izy9dp7wshOWVot.png)



# css border 属性设置

```html
<html>
    <head>
        <title></title>
        <style type = "text/css">
            div{
                border : 1px solid #000000;
            }
        </style>
    </head>
    <body>
        
    </body>
</html>
```

```css
border : 边框厚度 边框样式 边框颜色
//写成border是设置边框的四个边为统一格式，也可以分开设置
//border-top 上边框 border-bottom 下边框 border-left左边框 border-right 右边框
//边框样式:
//none : 无边框。与任何指定的border-width值无关
//dotted : 点线
//dashed : 虚线
//solid : 实线
//double : 双线边框
```

> 默认的边框颜色是元素本身的前景色。如果没有为边框声明颜色，它将与元素的文本颜色相同。另一方面，如果元素没有任何文本，假设它是一个表格，其中只包含图像，那么该表的边框颜色就是其父元素的文本颜色（因为 color 可以继承）。这个父元素很可能是 body、div 或另一个 table

# css margin 属性

* margin属性设置外边距

[做完题来补笔记](https://www.w3school.com.cn/cssref/index.asp)

# css font 属性(一定写在color属性前)

* 可以按照顺序设置如下属性:
  * font-style
  * font-variant
  * font-weight
  * font-size/line-height
  * font-family

# css padding 属性

* padding设置内边距

# css position属性

* 设置元素的定位方式
* [here](https://www.w3school.com.cn/cssref/pr_class_position.asp)