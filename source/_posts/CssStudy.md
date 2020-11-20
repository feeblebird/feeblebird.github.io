---
title: CssStudy
date: 2020-09-14 08:11:19
tags: css
categories: Web前端
---

# [参考手册](https://www.w3school.com.cn/cssref/index.asp)

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

* ![image.png](https://i.loli.net/2020/11/19/mUZj3siSBoEtPFJ.png)

* h1 {margin : 10px 0px 15px 5px;}

  与内边距的设置相同，这些值的顺序是从上外边距 (top) 开始围着元素顺时针旋转的：

  margin: top right bottom left

* 有时，我们会输入一些重复的值：

  p {margin: 0.5em 1em 0.5em 1em;}

  通过值复制，您可以不必重复地键入这对数字。上面的规则与下面的规则是等价的：

  p {margin: 0.5em 1em;}

  这两个值可以取代前面 4 个值。这是如何做到的呢？CSS 定义了一些规则，允许为外边距指定少于 4 个值。规则如下：

  如果缺少左外边距的值，则使用右外边距的值。

  如果缺少下外边距的值，则使用上外边距的值。

  如果缺少右外边距的值，则使用上外边距的值。

  下图提供了更直观的方法来了解这一点：

  ![image.png](https://i.loli.net/2020/11/19/A3Ft5sWijYXadOq.png)

  换句话说，如果为外边距指定了 3 个值，则第 4 个值（即左外边距）会从第 2 个值（右外边距）复制得到。如果给定了两个值，第 4 个值会从第 2 个值复制得到，第 3 个值（下外边距）会从第 1 个值（上外边距）复制得到。最后一个情况，如果只给定一个值，那么其他 3 个外边距都由这个值（上外边距）复制得到。

* 一个规则中可以使用多个这种单边属性，例如：

  h2 {
   margin-top: 20px;
   margin-right: 30px;
   margin-bottom: 30px;
   margin-left: 20px;
   }

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

# css设置div居中

```css
<style type="text/css">
		div{
			margin :0 auto;//居中
			text-align : center;//div中内容居中
			border : 1px solid;//设置边框厚度及边框样式
			width : 700px;//设置边框的宽度
            height:200px;//设置边框的高度
		}
	</style>
```

# css控制该区域内输出样式和代码一致

```css
<div style="white-space:pre"; id = "main">
	//即保留该区域内的空格，回车等等	
</div>
```

# css border-radius使用

* [参考](https://www.cnblogs.com/happymental/p/7891725.html)
* 通过设置元素的border-radius值，可以轻松给元素设置圆角边框，甚至实现绘制圆、半圆、四分之一的圆等各种圆角图形

* 三种使用方法：

  * px
  * %
  * em

* 只设置一个值，即给四个边框设置统一的值

  * ```css
    test1 {
        border: 3px solid red;
        height: 100px;
        width: 200px;
        border-radius: 30px;
    }
    ```

    ![image.png](https://i.loli.net/2020/11/04/dpNCuqaPhZQjG9Y.png)

  * ```css
    #test2 {
    　  border: 3px solid red;
    　　 height: 100px;
    　　width: 100px;
    　　border-radius: 53px;
    }
    ```

    ![image.png](https://i.loli.net/2020/11/04/aweMGNOJQqnPTvy.png)

  * 还可以单独设置每个角上边框的值

* 使用px表示数值的情况

  * 使用px的时候，圆角的弧度一般都是一个圆形的部分弧形

    > 假设一个长200px，高150px的div对象，设置它的border-radius的值为30px，那么实际呈现的圆角，其实就是一个以30px为半径的圆顶格放置在四个边角后所呈现的弧度

* 使用%表示数值的情况

  * 使用%来表示圆角值的时候，如果对象的宽和高是一样的，那判断方法与第一点一致，只不过想象的时候，需要将宽高乘以百分数换算一下
  * 如果宽高不一致，那产生的效果，其实就是以对象的宽高乘以百分数后得到的值r1和r2，作为两条半径绘制出来的椭圆产生的弧度

# text-decoration属性

```css
h1{text-decoration:overline;}
h2{text-decoration:line-through;}
h3{text-decoration:underline;}
h4{text-decoration:blink;}
```

* 效果如下：

![image.png](https://i.loli.net/2020/11/11/cLqpTCzktai8f1J.png)

# position 属性
关于CSS position，来自MDN的描述：
> CSS position属性用于指定一个元素在文档中的定位方式。top、right、bottom、left 属性则决定了该元素的最终位置。
然后来看看什么是文档流(normal flow)，下面是 [www.w3.org](https://www.w3.org/TR/CSS21/visuren.html#) 的描述：
> **Normal flow**
>
> Boxes in the normal flow belong to a formatting context, which may be block or inline, but not both simultaneously. [Block-level](https://www.w3.org/TR/CSS21/visuren.html#block-level) boxes participate in a [block formatting](https://www.w3.org/TR/CSS21/visuren.html#block-formatting) context. [Inline-level boxes](https://www.w3.org/TR/CSS21/visuren.html#inline-level) participate in an [inline formatting](https://www.w3.org/TR/CSS21/visuren.html#inline-formatting) context.

个人补充（此处参考[FungLeo](https://blog.csdn.net/fungleo)的博客文章，[原文点此](https://blog.csdn.net/fungleo/article/details/50056111)）：

1. normal flow直译为常规流、正常流，国内不知何原因大多译为文档流；
2. 窗体自上而下分成一行一行，并在每行中按从左至右的顺序排放元素；
3. 每个非浮动块级元素都独占一行， 浮动元素则按规定浮在行的一端，若当前行容不下，则另起新行再浮动；
4. 内联元素也不会独占一行，几乎所有元素(包括块级，内联和列表元素）均可生成子行，用于摆放子元素；
5. 有三种情况将使得元素脱离normal flow而存在，分别是 float，absolute ，fixed，但是在IE6中浮动元素也存在于normal flow中。

### 一、position: static

MDN的描述：

> 该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top、right、bottom、left 属性无效。

个人补充：static是position的默认值。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS-position-static</title>
    <link rel="stylesheet" href="https://cdn.bootcss.com/normalize/8.0.0/normalize.css">
    <style>
        .container{
            background-color: #868686;
            width: 100%;
            height: 300px;
        }
        .content{
            background-color: yellow;
            width: 100px;
            height: 100px;
            position: static;
            left: 10px;/* 这个left没有起作用 */
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="content">
        </div>
    </div>
</body>
</html>
```

![image.png](https://i.loli.net/2020/11/19/C2V8unlPwJsSOqp.png)

对 content 的 position 设定 static 后，left就失效了，而元素（content）就以正常的 normal flow 形式呈现。

### 二、position: relative

MDN的描述：

> 该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。position:relative 对 table-*-group, table-row, table-column, table-cell, table-caption 元素无效。

个人理解：相对于normal flow中的原位置来定位。

*  position: relative

![image.png](https://i.loli.net/2020/11/19/MsfKL9UjIkGoJg7.png)

这是没有设置left、top等属性时，正常出现在normal flow中的位置。

接着添加left、top：

```css
.content_1{
                background-color: red;
                width: 100px;
                height: 100px;
                position: relative;/* 这里使用了relative  */
                left: 20px;/* 这里设置了left和top */
                top: 20px;
            }
```

![image.png](https://i.loli.net/2020/11/19/bNsuw7PgE1oMcYj.png)

可以看到，元素（content_1）的位置相对于其原位置（normal flow中的正常位置）进行了移动。

### 三、position: absolute

MDN的描述

> 不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margin），且不会与其他边距合并。

个人理解：生成绝对定位的元素，其相对于 static 定位以外的第一个父元素进行定位,会脱离normal flow。**注意：是除了static外**

* position: absolute

![image.png](https://i.loli.net/2020/11/19/jP1gXywiFScLKCD.png)

因为 content 的父元素 container 没有设置 position，默认为 static，所以找到的第一个父元素是 body（\<body\>\</body\>），可以看成是元素（content）相对于 body 向下移动10px。

### 四、position: fixed

MDN的描述

> 不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed属性会创建新的层叠上下文。当元素祖先的 transform 属性非 none 时，容器由视口改为该祖先。

个人理解：fixed相对于window固定，滚动浏览器窗口并不会使其移动，会脱离normal flow。

* position: fixed

这里就不上图了，看一下代码或者自己动手码一下就能理解。

### 五、position: sticky

MDN的描述

> 盒位置根据正常流计算(这称为正常流动中的位置)，然后相对于该元素在流中的 flow root（BFC）和 containing block（最近的块级祖先元素）定位。在所有情况下（即便被定位元素为 table`时`），该元素定位均不对后续元素造成影响。当元素 B 被粘性定位时，后续元素的位置仍按照 B 未定位时的位置来确定。position: sticky对 table元素的效果与 position: relative 相同。

因为各大浏览器对于sticky的兼容问题，而且JS也可以实现这个功能，在这里就不进行深入了，了解一下就好。

### 六、position: inherit

[w3school.com](http://www.w3school.com.cn/cssref/pr_class_position.asp)的 描述

> 规定应该从父元素继承 position 属性的值。

inherit 继承父元素，这个用得不多，所以也不继续深入了。

# @keyframes 与 css animation属性配合

* 实例

  ```css
  @keyframes mymove
  {
  from {top:0px;}
  to {top:200px;}
  }
  /*要在要移动的标签的css中加上animation属性*/
  div{
      width:100px;
  	height:100px;
  	background:red;
  	position:relative;
  	animation:mymove 5s infinite;
  }
  ```

* 可以利用@keyframes实现动画播放效果

  ```html
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  	<style type="text/css">
  		#love1{
  			width:50px;
  			height:50px;
  			margin:300px auto;
  			position: relative;
  			/*bottom:1050px;*/
  			animation: mymove 2s infinite;
  		}
  		#love2{
  			width:50px;
  			height:50px;
  			bottom:700px;
  			margin:300px auto;
  			position: relative;
  			animation: mymove 2s infinite;
  		}
  		#love3{
  			width:50px;
  			height:50px;
  			bottom:350px;
  			margin:300px auto;
  			position: relative;
  			animation: mymove 2s infinite;
  		}
  		#love4{
  			width:50px;
  			height:50px;
  			margin:300px auto;
  			position: relative;
  			animation: mymove 2s infinite;
  		}
  		.l{
  			width:30px;
  			height:30px;
  			background:red;
  			border-radius:50%;
  			left:0px;
  			top:0px;
  			position:absolute;
  		}
  		.r{
  			width:30px;
  			height:30px;
  			background:red;
  			position:absolute;
  			border-radius:50%;
  			right: 0px;
  			top:0px;
  		}
  		.z{
  			width:30px;
  			height:30px;
  			background:red;
  			transform:translate(10px,10px) rotate(45deg);
  		}
  		@keyframes mymove{
  			0%{
  				transform:scale(1);
  			}
  			50%{
  				transform:scale(1.5);
  			}
  			100%{
  				transform:scale(1);
  			}
  		}
  		@keyframes mymove2{
  			from{
  				left:0px;
  				transform:scale(1);
  			}
  			to{
  				left:-100px;
  				transform:scale(1);
  			}
  		}
  	</style>
  </head>
  <body>
  	<div id = "love4">
  		<div class="l"></div><div class="r"></div>
  		<div class="z"></div>
  	</div>
  	<div id = "love3">
  		<div class="l"></div><div class="r"></div>
  		<div class="z"></div>
  	</div>
  	<div id = "love2">
  		<div class="l"></div><div class="r"></div>
  		<div class="z"></div>
  	</div>
  	<div id = "love1">
  		<div class="l"></div><div class="r"></div>
  		<div class="z"></div>
  	</div>
  
  	<script type="text/javascript">
  		document.getElementById("love1").onclick=function(){
  			document.getElementById("love1").style.animation="mymove2 2s 1";
  			window.setTimeout("next()",2000);
  		}
  		window.next=function(){
  			document.getElementById("love1").style.animation="mymove 2s infinite";
  			document.getElementById("love1").style.left="-100px";
  		}
  	</script>
  </body>
  </html>
  ```

# transform scale

**scaleX()**

***\*scaleY()\****

　　缩放该元素，>1 放大， <1 缩小 默认值是 1；

![image.png](https://i.loli.net/2020/11/19/jBlNuJaeRgTO2c5.png)

 

看了上面的图，你可能会觉得，好像是100px 变成了200px  但是实际上，并不是。变的不是 元素的 宽高。

![image.png](https://i.loli.net/2020/11/19/b5hTr6NlHQFtqf7.png)

其实，他改变的不是元素的宽高，而是x 和 y 轴的刻度 ↓ 

![image.png](https://i.loli.net/2020/11/19/piM4JYums9ra61L.png)

 

**scale()**

这个呢，是上面两个的合体，也就是 参数 第一个是x 第二个是y

![image.png](https://i.loli.net/2020/11/19/gc4osJ2wRALIFmD.png)

![image.png](https://i.loli.net/2020/11/19/h8DInViNWxuX35v.png)

 

**scale3d()**

第一个参数是 x 第二个参数是y 第三个参数是z ，也就是scalex scaley scalez 的结合体。

scalez吧，这个值原本就是3D的，所以可能会有点难理解， 像上面这个图， 本来就是2D 的图，你再怎么拉伸他的Z 轴，也是看不出效果的。前提是你的图，是3D的才能拉伸，2D的是拉伸不了的。 如果有不知道Z轴在哪里的朋友，请点这里→ [
](https://www.cnblogs.com/yanggeng/p/11277199.html#Z)

**探索：**

首先，我们来思考一个问题，使用 rotate进行旋转，那么 X 和 Y 轴是会跟着旋转而变化的，那么这个时候加上 scaleX 和 Y，那么旋转的过程中，会不会带上scale 的效果？

先来观察一下， 先rotate 再 scale 的效果：

[看图](https://img2018.cnblogs.com/blog/1609428/201907/1609428-20190731163906364-1545153301.gif)

看完上面的图，是不是觉得，旋转的时候，会带着scale的效果一起旋转。 但是！ 如果把他俩位置换了，那结果是截然不同的，先scale 再 rotate

[看图](https://img2018.cnblogs.com/blog/1609428/201907/1609428-20190731164301719-2014901299.gif)

对比两张图，你就会发现，第一张的效果，确实是带上了scale的效果一起旋转的，怎么 换了个位置，就不一样呢？

其实呢，先rotate，再scale(先旋转，后缩放) 是会把效果带上旋转的，但是 先scale 再rotate(先缩放，后旋转) 是不会把缩放的效果带上旋转的，缩放的效果，会留在原地，等你经过的时候，就会生效。看下面的图解，缩放的比例，会留在原地，经过的时候，就会恢复比例。

[看图](https://img2018.cnblogs.com/blog/1609428/201907/1609428-20190731165325626-360527648.gif)

# display属性

* none为不显示
* block为显示为块级别，后面带换行符

[补笔记](https://www.w3school.com.cn/cssref/pr_class_display.asp)

# css实现图片等比例缩放并居中

```css
#main{
			width:200px;
			height:220px;
			margin:250px auto;
			border: 1px solid red;
			display: flex;
			justify-content: center;
			align-items:center;
		}
		#main img{
			width:auto;
			height: auto;
			max-width: 200px;
			max-height: 220px;
			text-align: center;
		}
```

[参考](https://blog.csdn.net/qq_43258252/article/details/88895337)







