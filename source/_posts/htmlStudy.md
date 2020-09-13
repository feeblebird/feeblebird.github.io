---
title: htmlStudy
date: 2020-09-13 09:16:55
tags: html
categories: Web前端
---

# 标签分为双标签和单标签

* #### 标题标签  双标签

  ```html
  <h1>
      
  </h1>
  <!--h1到h6字体逐渐从大到小-->
  <h6>
      
  </h6>
  ```

* #### 段落标签  双标签 paragraph

  ```html
  <p>
      
  </p>
  <!--段落之间的间隔比不是段落之间的间隔大-->
  ```

* #### 水平线标签 单标签 hrizontal

  ```html
  <hr />
  ```

* #### 换行标签 单标签 break

  ```html
  <br />
  ```

* #### 分块标签 

  ```html
  <div>
      
  </div>
  <span>
      
  </span>
  ```

* #### 字体效果标签

  * 加粗

    ```html
    <s></s>
    <strong></strong>
    ```

  * 斜体

    ```html
    <i></i>
    <em></em>
    ```

  * 删除线

    ```html
    <s></s>
    <del></del>
    ```

  * 下划线

    ```html
    <u></u>
    <ins></ins>
    ```

* #### 标签的属性统一格式: 标签属性 = "属性值"

* #### 图像标签 单标签 image

  ```html
  <img src = "url" alt = "" title = "" width = "" height = "" border = "" />
  <!--
  src : 图片来源，可以是相对路径，也可以是绝对路径，但一般不推荐使用绝对路径
  alt : 如果图片无法正常显示，则用这个文本替换它
  title : 鼠标悬停在图片上时所显示的文本内容
  width , height : 调整宽度和高度
  border : 给图片添加边框
  -->
  ```

* #### 链接标签 双标签 anchor

  ```html
  <a href = "跳转目标" target = "_self"/"_blank">文本或图像</a>
  <!--
  href : 跳转的链接，跳转目标中要带上协议名称。
  href = "filename.html"可以跳转到自己写的另一个页面
  href = "#" 没有确定的跳转目标
  target : _self是覆盖原来页面 _blank是用新标签页打开
  -->
  ```

* #### 锚点链接 双标签 anchor

  ```html
  <a href = "#编号">图像或文字</a>
  <!--那个编号可以在别的标签中的id属性进行声明-->
  <h3 id = "编号">
      
  </h3>
  <p id = "编号">
      
  </p>
  ```

* #### base标签 单标签 设置统一打开方式为"_blank"

  ```html
  <head>
      <base target = "_blank"/>
  </head>
  ```

* #### 特殊字符表示方式

  ![特殊字符](https://i.loli.net/2020/09/13/K3cnB4lpohjNGMd.png)

* #### 注释标签

  ```html
  <!--注释内容-->
  ```

* #### 列表标签 有序和无序和自定义 双标签

  ```html
  <ol>
      <li></li>
      <li></li>
  </ol>
  <ul>
      <li></li>
      <li></li>
  </ul>
  <dl>
      <dt>名词</dt>
      <dl>
          解释
      </dl>
      <dl>
          解释
      </dl>
  </dl>
  ```

* #### 表格标签 双标签 table

  ```html
  <table width = "" height = "" border = "" cellspcing = "" cellspadding = "" align = "center/right/left">
  <!--
  border:边框厚度
  cellspacing:边框距离
  cellspadding:文字距离左边框距离
  align:表格的水平对齐方式，里面的文字还是在左边
  -->
      <tr> <!--一行-->
      	<td></td> <!--一个单元格-->
          <td></td>
      </tr>
  </table>
  ```
  > 把\<td\>\</td\>换成\<th\>\</th\>就会将文字居中并加粗

  ```html
  <table>
      <thead> <!--标识出这是表格关键字内容-->
          <tr>
          	<td></td>
              <td></td>
          </tr>
      </thead>
      <tbody> <!--标识出这是表格主体内容-->
          <tr>
          	<td></td>
              <td></td>
          </tr>
      </tbody>
  </table>
  ```

  ```html
  <table>
      <caption>表格标题</caption>
      <!--这个标题会随着表格一起移动-->
  </table>
  ```
  
  ```html
  <!--表格合并单元格,合并的顺序是从上到下，从左到右-->
  <td rowspan = "合并的个数"></td> <!--表示这个单元格所占的行数-->
  <td colspan = "合并的个数"></td> <!--表示这个单元格所占的列数-->
  ```
  
* #### 表单标签 input空间 单标签

  * 输入标签

  ```html
  <input />
  ```

  * 属性值

    ![input空间属性值](https://i.loli.net/2020/09/13/MTJ7Ddug2AtrwLG.png)

  * 文本框

    ```html
    <input type = "text"/>
    ```

  * 单选框

    ```html
    <input type = "radio" name = "名字" />选项内容1
    <input type = "radio" name = "名字" checked = "checked"/>选项内容2
    <!--同一个name的单选互斥,checked属性默认勾选这个选项-->
    ```

  * 复选框

    ```html
    <input type = "checkbox" name = "名字" />
    <!--名字会在提交的时候用上-->
    ```

  * 图片按钮

    ```html
    <input type = "image" src = "" />
    ```

  * input空间中的默认文本值，最大输入字数

    ```html
    <input type = "" value = "" maxlength = ""/>
    ```

  * 上传文件

    ```html
    <input type = "file" />
    ```

* #### label标签 实现点击文字即可输入文本的效果

  ```html
  <label>输入:<input type = "txt" /></label>
  <label for = "two">
     	输入:<input type = "txt" />
  	输入:<input type = "txt" id = "two"/>
  </label>
  ```

* #### 文本域标签 双标签

  ```html
  <textarea></textarea>
  ```

* #### 下拉菜单 双标签

  ```html
  <select>
      <option>选项1</option>
      <option>选项2</option>
      <option>选项3</option>
      <option selected = "selected">选项1</option>
      <!--默认选项-->
  </select>
  ```

  

