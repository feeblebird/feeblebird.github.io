---
title: CssStudy
date: 2020-09-14 08:11:19
tags: css
categories: Web前端第三个第四个
---

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

* 选择符通常是通配选择符、标记选择符、包含选择符、ID选择符、类选择符和选择符分组。

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

  