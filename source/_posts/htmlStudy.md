---
title: htmlStudy
date: 2020-09-13 09:16:55
tags: html
categories: Web前端
---

# [参考手册](https://www.w3school.com.cn/tags/index.asp)

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

  * 加粗 bold

    ```html
    <b></b>
    <strong></strong>
    ```

  * 斜体 italic

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
  href = "#" 没有确定的跳转目标,表示回到顶部
  target : _self是覆盖原来页面 _blank是用新标签页打开
  -->
  ```

  ##### href ="URL"的作用

  * URL为绝对URL

    指向另一个站点，点击后就会直接跳转到这个链接的页面

  * URL为相对URL

    指向站点内的某个文件，比如`href="/test.doc"` 那么点击时就会直接下载文件

  * 锚URL

    此时指向页面中的锚，比如`href="#top"` 那么点击时就会到当前页面中`id="ttip"` 的这个锚点，实现当前页面的所谓跳转。用的最多的就是在可滚动页面中，添加菜单，可以直接回到页面中的某个部分的内容。

    `href="#"` 的时候就是回到顶部

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

  * > 注意reset按钮必须放在\<form\>\</form\>中才起作用

  * 属性值

    ![input空间属性值](https://i.loli.net/2020/09/13/MTJ7Ddug2AtrwLG.png)

    * 属性值还有hidden，将该输入标签隐藏，可以通过这个传递不想让用户修改的post数组内容

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
  <label>输入:<input type = "text" /></label>
  <label for = "two">
     	输入:<input type = "text" />
  	输入:<input type = "text" id = "two"/>
  </label>
  ```

* #### 文本域标签 双标签

  ```html
  <textarea></textarea>
  隐藏调节大小的按钮
  <textarea style = "resize:none"></textarea>
  用css的内容
  
  文本域不填写内容是空字符串""，不是位null
  ```

* #### 下拉菜单 双标签 可用datalist代替使用

  ```html
  <select>
      <option>选项1</option>
      <option>选项2</option>
      <option>选项3</option>
      <option selected = "selected">选项1</option>
      <!--默认选项-->
  </select>
  ```

* #### 表单域

  ```html
  <form action = "xxx.php" metho = "post" name = "user">
      <input /><!--等等-->
  <!--
  action:将数据提交到某某后台,此时提交和充值按钮都开始起作用
  method:提交方式 
  -->
  </form>
  ```

* #### html发展大概历史

  ![](https://i.loli.net/2020/09/13/EkCtWfVA64lUK39.png)


# html5常用新标签

* #### header 定义页眉 双标签

  ```html
  <header></header>
  ```

* #### 导航栏 nav 双标签

  ```html
  <nav></nav>
  ```

* #### 页面底部 footer 双标签

  ```html
  <footer></footer>
  ```

* #### 定义文章 article 双标签

  ```html
  <article></article>
  ```

* #### section 定义文章中的小节、区、块 双标签

  ```html
  <section></section>
  ```

* #### aside 定义侧边块 双标签

  ```html
  <aside></aside>
  ```

* #### datalist 定义选项列表，与input元素配合使用，可替代select

  显示效果为输入某个字时，会提示已有结果

  ```html
  <input type = "text" value = "输入明星" list = "star"/>
  <datalist id = "star">
      <option>刘德华</option>
      <option>刘德华</option>
      <option>刘德华</option>F
      <option>刘德华</option>
  </datalist>
  ```

* #### fieldset元素可将表单内的相关元素分组，打包与legend搭配使用

  ```html
  <fieldset>
      <legend>
          用户登录
          用户名:<input type = "text"/>
          密码:<input type = "password"/>
      </legend>
  </fieldset>
  ```

# html5新增input属性

![](https://i.loli.net/2020/09/13/JcBowEYOzCfDjtV.png)

* #### type

  ```html
  <form>
      邮箱:<input type = "email" />
      手机:<input type = "tel" />
      数字:<input type = "number" />
      url:<input type = "url" />
      搜索:<input type = "search" />
      拖动滑块:<input type = "range" />
  </form>
  ```

* #### 时间属性

  ```html
  <form>
      时间:<input type = "time" />
      date:<input type = "date" />
      datetime:<input type = "datetime" />
  </form>
  ```

* #### 搜索框默认文本默认内容，输入又消失，占位符

  ```html
  <input type = "text" placeholder = "请输入"/>
  ```

* #### 页面加载自动获得焦点，即加载后光标自动选择

  ```html
  <input type = "text" placeholder = "请输入" autofocus />
  <input type = "text" placeholder = "请输入" autofocus = "autofocus" />
  ```

* #### 上传多个文件

  ```html
  <input type = "file" multiple />
  <input type = "file" multiple = "multiple" />
  ```

* #### 自动记录

  ```html
  <form action = "">
      <!--使用自动记录，首先需要提交按钮，然后需要给表单name值-->
      <input type = "text" autocomplete name = "username"/>
      <input type = "text" autocomplete = "autocomplete" name = "username"/>
      <input type = "text" autocomplete = "on" name = "username" />
      <input type = "text" autocomplete = "off" name = "username" >
      <!--关闭自动记录功能-->
      <input type = "submit" />
  </form>
  ```

* #### 必填项(内容不为空)

  ```html
  <form action = "">
      <input type = "text" required />
  </form>
  ```

* #### accesskey自动跳转

  ```html
  <form action = "">
      <input type = "text" accesskey = "s" />
      <!--按下alt + s 则自动跳转到这个文本框进行输入-->
  </form>
  ```

# 多媒体标签

* #### 插入音频

  ```html
  <audio src = "xxx.mp3"></audio> <!--不自动播放-->
  <audio src = "xxx.mp3" autoplay = "autoplay"></audio><!--自动播放-->
  <audio src = "xxx.mp3" autoplay = "autoplay" controls></audio>
  <!--显示控制组件-->
  <audio src = "xxx.mp3" loop = "2"></audio>
  <!--loop = n循环唱n次 等于-1时，无限安循环-->
  ```

* #### 为了不同浏览器的兼容，上传两种格式

  ```html
  <audio autoplay = "autoplay" controls>
  	<source src = "xxx.mp3" />
      <source src = "xxx.ogg" />
  </audio>
  ```

* #### 插入小视频

  ```html
  <video src = "xxx.mp4/xxx.ogg/xxx.WebM" autoplay controls width = "" ></video>
  ```

* #### 为了不同浏览器的兼容

  ```html
  <video controls autoplay>
  	<source src = "xxx.mp4"/>
      <source src = "xxx.ogg"/>
  </video>
  ```


# meta标签

* #### meta标签没有结束标签

  ```html
  <meta charset = "utf-8">
  ```

  