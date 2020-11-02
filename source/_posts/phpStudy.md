---
otitle: phpStudy
date: 2020-09-22 08:36:55
tags: php
categories: php
---

# [参考手册](https://www.w3school.com.cn/php/php_intro.asp)

# php文件放入xampp中htdoc目录下

# 使用，输出时间

```php
<html>
    <body>
        <?php
			echo "<p>今天是 ";
			date_default_timezone_set("PRC");
			echo date("Y年m月d日H:i:s D");//小写d几号，大写D周几
		?>
    </body>
</html>
```

# php注释为//单行注释，/**/多行注释

# echo、print、print_r、var_dump

```php
<?php
    echo "<h2>内容</h2>";
    //将内容传送到html服务端进行解释
	echo "i","am","liwei";
	//可以一次输出多个字符串,以","连接
    echo ("内容");
	echo ($b);
	echo("i"."am"."liwei");
	echo "var=".$var."<br />";
	//使用()输出多个字符串，中间用.进行连接，"."为字符串连接符
	print "";
	print("内容");
?>
```

> print使用方法与echo相同，不同的地方是print有返回值，返回值始终为1。
>
> 所以使用过程中echo比print稍快，因为没有返回值

> print_r输出数组
>
> var_dump输出数据类型和变量的值

> echo 和 print 打印不出boolean的"true"和"false"
>
> true会打印出1,false会被认为是空

# 大小写问题

* 对自定义的变量名称大小写是敏感的

* $+变量名，首次赋值的时候就会被创建( **是紧跟，不加空格** )

  $a = 123;

* 对关键字大小写不敏感

# 数据类型

* 标量类型
  * boolean
  * integer
  * float/double
  * string
    * $first = "hello";
    * $first = 'hello';
    * $first = "hell"."o";
* 复合型
  * array
  * object
* 特殊类型
  * resource
  * NULL

# string 三种引号的使用

* #### 单引号括起来就是字符串

  * 含有单引号的话，就知识被认为是字符串

* #### 双引号括起来

  * 表示字符串
  * 特殊字符转义序列，"\n"
  * 含有变量，则会显示变量的值

* 打印单引号，使用双引号

  ```php
  echo "i'm liwei";
  ```

* 打印双引号，使用单引号

  ```php
  echo '"它"是啥';
  ```

* 打印双引号，使用双引号

  * 使用转义字符

  ```php
  echo "hello \" 哈哈哈";
  ```

* #### 反引号

  使用反引号括起来可以运行系统命令。

# 类型转换

* #### 自动类型转换

  * 赋值转换

  ```php
  <?php
  	$a = 1;
  	$a = "string";
  //尽量一个变量存放的数据类型是固定的
  ?>
  ```

  * 表达式转换(临时转换，不改变原先变量数据类型)

  ```php
  <?php
  	$a = "100";
  	$b = $a*2;
  //自动把a变量转换称integer
  	echo ($b);
  ?>
  ```

  * 强制类型转换
    * (int),(integer)
    * (bool),(boolean)
    * (float),(double),(real)
    * (string)
    * (array)
    * (object)

# 变量的作用域

* 声明局部变量

  在函数内部声明变量

* 声明全局变量

  在函数外部声明变量为全局变量

  * 若要在函数内部使用全局变量

    要先在函数内部声明该变量为全局变量，global + $ + 变量名;

* 声明静态变量

  static $var = value;

  在函数外部任然存在，不会被销毁

#  声明可变变量名

  用变量值作为变量名

```php
  $var_name = "myvar";
  $$var_name = 10;
```

# 常量

* 自定义常量

  define("constname","value");

* 系统常量
  * \_\_FILE\_\_( **两个下划线** )输出文件名，总是包含绝对路径
  * \_\_LINE\_\_( **两个下划线** )输出文件行数
    * 魔术常量，值随着代码中的位置改变而改变

# 运算符

* 算数运算符

  就是学过的

* 逻辑运算符

  * && /and
  * || / or
  * xor

* 比较运算符

  * ==，值相等就返回true,数据类型可以不同
  * ===，值相同且数据类型也相同
  * !=，值不等
  * !==，值不等或数据类型不等

* 其他运算符

  * .
  * $
  * @，错误控制运算符
    * 在表达式之前加上@，则不会提示该句引起的错误
    * 自定义错误输出
  * \$a>\$b?$a++:\$a--; 三重运算符

# if、while、for、do...while

```php
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style>
		td{
			border : 1px solid #ccc;
			padding : 3px;
			text-align : right;
		}
		th{
			background : #ccc;
		}
	</style>
</head>
<body>
	<table>
		<tr>
			<th>
				distance
			</th>
			<th>
				price
			</th>
		</tr>
		<?php 
			$distance = 50;
			while($distance <= 300)
			{
				$price = $distance/10;
				echo "<tr><td>".$distance."</td><td>".$price."</td></tr>";
				$distance = $distance + 50;
			}
		?>
	<table>
</body>
</html>
```

# 以html文件为主，然后再写入php代码

> 当php周围代码很复杂的时候，可以这样写

```php+HTML
<html>
    <head>
        <tithle></tithle>
    </head>
    <body>
        <table>
            <tr><th>Distance</th><th>Cost</th></tr>
            <?php
				$distance = 50;
				while($distance <= 250)
				{                //没有结束大括号，继续向后执行  
			?>
            <tr>
                <td><?php echo ($distance) ?></td>
                <td><?php echo ($distance/10) ?></td>
            </tr>
            <?php
				$distance += 50;
                }
			?>
        </table>
    </body>
</html>
```

# 数组 array()

* array()定义数组

* 赋值

  * $arr = array("111","222",..."nnn");
  * $arr[0] = "111";...

* 获得数组长度

  * $length = count(\$arr);

* 自动添加到尾部(即最后一个元素的下标加一 )

  * $arr[] = "string"; 

* 直接往数组中插入一个元素且指定下标元素

  * 但是中间没有赋值的元素无法输出
  * 这样的话就不能用for循环进行遍历，因为下标变化是连续的
  * 这时使用foreach

  ```php
  foreach($arrname as $key => $value)
  {
      //as后面 key存储下标	 value存储对应的值
      echo "$value";
  }
  ```

* php中的数组下标可以为其他类型

  ```php
  $b = array("name"=>"jessie","city"=>"lanzhou","age"=>"10");
  $b["sex"] = "famale";
  ```

# 二维数组

```php
$a = array(
	"地支" => array("子","丑","鄚"),
    "天干" => array()
);
```

* 输出二维数组

```php
foreach($b as $key => $value){
			echo "$key: ";
			foreach($value as $key1 => $value1)
			{
				echo "$key1 is $value1 &nbsp&nbsp&nbsp&nbsp";
			}
			echo "<br />";
}
```

# 数组排序函数

* sort()：以升序对数组排序
* rsort()：以降序对数组排序

> 用sort()和rsort()进行的排序，输出下表时会只输出0，1，2，...不会输出自定义的下标
>
> 本函数会为排序的数组中的单元赋予新的键名，这将删除原有的键名而不仅是重新排序。
>
> 如果要输出自定义的下标，要使用下面的这四个排序函数

* asort()：根据值，以升序对关联数组进行排序

* ksort()：根据键，以升序对关联数组进行排序

* arsort()：根据值，以降序对关联数组进行排序

* krsort()：根据键，以降序对关联数组进行排序

* #### sort()、ksort()、asort()、rsort()的异同点

> 相同点：sort、ksort、asort都能对数组进行升序排序
>
> 不同点：sort排序在输出的时候会重新给键赋值为0~n-1，而原来的键值对没有变还能继续赋值等等，而ksort、asort在输出时都会输出原来的键值对。
>
> rsort是降序排序，与sort类似
>
> 都由第二个参数sortingtype指定排序类型，ksort默认把键值转换为int型来排序，asort默认把值转换为字符串类型来排序。
>
> 

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<?php
		$arr = array("bill"=>"a","steve"=>"b","elon"=>"c");
		asort($arr);
		echo "根据值进行升序排序<br />";
		foreach($arr as $key => $value)
		{
			echo "key: ".$key." value:".$value."<br />";
		}
		ksort($arr);
		echo "<br />根据键进行升序排序<br />";
		foreach($arr as $key => $value)
		{
			echo "key: ".$key." value:".$value."<br />";
		}
	?>
</body>
</html>
```

# php实现随机显示7张图片中的三张图

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type="text/css">
		#pics img{
			width : 200px;
		}
		#pics div{
			float : left;
			margin : 10px;
			padding : 5px;
		}
	</style>
</head>
<body>
	<div id = "pics">
		<?php
			$arr = array("1.jpg","2.png","3.png","4.png","5.png","6.jpg","7.jpg");
			shuffle($arr);
			for($i = 0;$i < 3;$i ++)
			{
		?>
				<div><img src = "myimages/<?php echo "$arr[$i]"; ?>"kj/></div>
		<?php
			}
		?>	
	</div>
</body>
</html>
```

> 图片放在本地的myimages目录下

# 函数

与其他语言类似。

# 引用文件--require()和include()

```php
require 'prepend.php';
require $somefile;
require('.txt');
```

* 两个函数对于错误处理
  * require会生成致命错误并停止脚本，用@屏蔽错误提示后，后面一片空白，上面的内容还能解释。
  * include只会生成一个警告，后面的内容还会解释。

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type = "text/css">
		#footer{
			width : 100%;
			height : 30px;
			background : #25506b;
			text-align : center;
			font-size : 12px;
			padding : 8px;
		}
	</style>
</head>
<body>
    <h1>
        这是一个示例
    </h1>
	<?php
		include "shangke.php";
	?>
</body>
</html>
```

* shangke.php文件

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<div id = "footer">
		<p>Copyright &copy; 2005-2020 兰州大学 All Rights Reserved</p>
	</div>
</body>
</html>
```

# 超全局变量

* _SERVER数组

  * 里面存放了很多服务器和用户信息

  ```PHP+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		$_SERVER["NAME"] = "兰州大学";//只会在当前进程中的所有数组插入该键值对，包括对引入文件中的该数据也起作用
  		echo "<pre>";
  		print_r($_SERVER);
  		echo "</pre>";
  		echo "您来自于".$_SERVER["REMOTE_ADDR"];
      	include "shangke.php";
  	?>
  </body>
  </html>
  ```

  * shangke.php中的内容

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		echo "<pre>";
  		print_r($_SERVER);
  		echo "</pre>";
  	?>
  </body>
  </html>
  ```

* _GET数组

  * 通过URL里面的参数来传递数据

  ```php+HTML
  $_GET['id']和$_GET['name']访问GET数据
  //注意中文乱码问题，使用urlencode编码
  
  //study.html文件
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<a href = "study.php?id=3">information</a>
  </body>
  </html>
  
  //shangke.php文件
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		include "study.html";
  	?>
  </body>
  </html>
  
  //study.php文件
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  	<style type = "text/css">
  		#footer{
  			width : 100%;
  			height : 30px;
  			background : #25506b;
  			text-align : center;
  			font-size : 12px;
  			padding : 8px;
  		}
  	</style>
  </head>
  <body>
  	<?php
  		$_SERVER["NAME"] = "兰州大学";
  		echo "<pre>";
  		print_r($_SERVER);
  		echo "</pre>";
  		echo "您来自于".$_SERVER["REMOTE_ADDR"];	
  		include "shangke.php";
  				echo "<pre>";
  		print_r($_GET);
  		echo "</pre>";
  	?>
  </body>
  </html>
  ```

  * 判断是否为空

  ```php+HTML
  if(empty($_GET))
  {
  	echo "no information";
  }
  //防止其他用于直接访问该网页，而url中没有参数而出现错误
  ```

  * get不适用表单传递，因为敏感信息会出现在地址栏中
  * get适合于收藏夹情况，因为把具体的参数都保存了，不然每次都是去首页

  ```php+HTML
  //study.html
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<a href = "study.php?id=3">information</a>
  	<form action = "study.php" method = "get">
  		用户: <input type = "text" name = "username"/>
  		<br />
  		密码: <input type = "password" name = "password"/>
  		<br />
  		<input type = "submit" name = "sub" />
  	</form>
  </body>
  </html>
  
  //shangke.php
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		include "study.html";
  	?>
  </body>
  </html>
  
  //study.php
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  	</style>
  </head>
  <body>
  	<?php
  		echo "<pre>";
  		print_r($_GET);
  		echo "</pre>";
      	echo ($_GET["username"]);
      	//或者  "$_GET[username]"
  	?>
  </body>
  </html>
  ```

  > 这里有个小问题，就是但就取get数组的值的时候，就是$_GET["username"]。
  >
  > 但是再后面的数据库插入$_POST数组的值的时候就是

  ```php
  $is = $conn->query("INSERT INTO `user`(`username`, `pwd`, `age`, `Gender`, `email`) VALUES ('$_POST[username]','$_POST[pawd]','$_POST[age]','$_POST[sex]','$_POST[email]')");
  ```

  

* 表单传递用_POST数组，信息不会出现在地址栏中

  ```php+HTML
  //study.html
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<a href = "study.php?id=3">information</a>
  	<form action = "study.php" method = "post">
  		用户: <input type = "text" name = "username"/>
  		<br />
  		密码: <input type = "password" name = "password"/>
  		<br />
  		<input type = "submit" name = "sub" />
  	</form>
  </body>
  </html>
  
  //shangke.php
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		include "study.html";
  	?>
  </body>
  </html>
  
  //study.php
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  	</style>
  </head>
  <body>
  	<?php
  		echo "<pre>";
  		print_r($_POST);
  		echo "</pre>";
  	?>
  </body>
  </html>
  ```


# post传递复选框的内容

* 要给复选框的name取名位name[]，才能正确传递。

# 从_POST数组中，输出复选框内容

```sql
echo "最不满意的食品 : ";
foreach ($_POST["food2"] as $key => $value) {
	echo "$value ";
}
echo "<br />";
```

# 判断表单中内容

```sql
<script type="text/javascript">
		function check()
		{
			if(tellsome.value == "")
			{
				tellsome.value = "无建议";
			}
		}
</script>
```

# _request数组(不建议初学者使用)

* 既可以接受post数据，也可以接受get数据
* 即可以在action加上参数，也可以接受表单提交的数据(method = "post")
* 且容易被别人利用漏洞攻击，所以实际中根据实际情况使用get和post

# web数据库工作原理

* 用户web浏览器发出http请求
* web服务器接受请求，读取文件并发送给php引擎处理(对接数据库的操作是在php中进行的)
* php引擎解析脚本
* mysql数据库接受并执行数据库指令、返回结果给php引擎
* php执行脚本结束，格式化查询结果，发送html至web服务器
* web服务器将html返回给浏览器

# php的mysql数据库函数

* 实现连接数据库、执行sql语句、返回查询结果
* 即下面这些

# php_mysql扩展库

* mysql扩展库已经停用，因为不能满足最新要求
* 先使用php_mysqli.dll,php_pdo_mysql等

# mysqli(增强版扩展库)

* 面向对象接口
* 面向过程接口

> 为了面向不同的使用习惯

* 连接数据库

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		$mysqli = new mysqli('localhost','my_user','my_password','my_db');
  		$mysqli = new mysqli(数据库地址，用户名，密码，数据库名);
  	?>
  </body>
  </html>
  ```
  
  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head >
  	<title></title>
  </head>
  <body>
  	<?php
  		$host = "localhost";
  		$username = "root";
  		$password = "li33092728li";
  		$database = "test";
      	$port = "13140";//尤其是更换过默认端口的需要自己指定端口
  		$conn = @new 
          mysqli($host,$username,$password,$database,$port);
      //@符号位忽略报错信息
  		if($conn->connect_errno){
  			die("数据库连接错误".$conn->connect_error);
  		}else{
  			echo "数据库连接成功";
  		}
  	?>
  </body>
  </html>
  ```

# 三码合一:数据库、页面、PHP代码

* 存储的编码问题
* 通信的编码问题（可能默认情况下不是utf-8编码）

```php+HTML
<!DOCTYPE html>
<html>
	<head >
		<title></title>
		<meta charset="utf-8" />
	</head>
	<body>
        <?php
        	header("Content-type: text/html;charset = utf-8");
        	$host = "localhost";
            $username = "root";
            $password = "li33092728li";
            $database = "test";
            $port = "13140";//尤其是更换过默认端口的需要自己指定端口
            $conn = @new 
            mysqli($host,$username,$password,$database,$port);
        //@符号位忽略报错信息
            if($conn->connect_errno){
                die("数据库连接错误".$conn->connect_error);
            }else{
                echo "数据库连接成功";
            }
        	$conn->query("set names utf8");//注意这里是utf8，不是utf-8
        //而且这个编码的设置针对写库的操作的，所以要放在插入数据语句的前面
        ?>
	</body>
</html>
```

# php向数据库插入数据

```php+HTML
<!DOCTYPE html>
<html>
<head >
	<title></title>
	<meta charset="utf-8" />
</head>
<body>
	<?php
		header("Content-type: text/html;charset = utf-8");
		$host = "localhost";
		$username = "root";
		$password = "li33092728li";
		$database = "test";
		$port = "13140";
		$conn = @new mysqli($host,$username,$password,$database,$port);
		if($conn->connect_errno){
			die("数据库连接错误".$conn->connect_error);
		}else{
		?>
			<script type="text/javascript">
				alert("数据库连接成功");
			</script>
		<?php
		}
		$conn->query("set names utf8");
		$is = $conn->query("INSERT INTO `user`(`ID`, `username`, `pwd`, `age`, `Gender`, `email`) VALUES ('1','liwei','111',12,'男','20113@qq.com')");
    	if($is)
        {
            ?>
    			<script type="text/javascript">
    				alert("插入数据成功");
    			</script>
    		<?php
        }else
        {
        	?>
    			<script type="text/javascript">
    				alert("插入数据失败");
    			</script>
    		<?php
        }
	?>
</body>
</html>
```

> 数据表用反引号，字段名用反引号括起来

# 向数据库中插入表单中收集的信息

* 表单内容

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<meta charset="utf-8" />
	<style type="text/css">
		div{
			margin :0 auto;
			text-align : center;
			border : 1px solid;
			width : 700px;
		}
	</style>
	<script type = "text/javascript">
		function judge()
		{
			var v1 = document.getElementById("2");
			var v2 = document.getElementById("3");
			if(v1.value != v2.value)
			{
				window.alert("两次密码不一致");
			}
		}
		function rese()
		{
			alert("输入的数据将被清空，你确定吗？")
		}
	</script>
</head>
<body>
	<div style="white-space:pre"; id = "main">
		<h2>用户注册</h2>
		<form action = "study.php" method = "post">
		用  户  名：	<input type = "text" name = "username" required="required" placeholder="请输入用户名" />
		<br/>
		密       码：	<input type = "password" id = "2" name = "pawd" required="required"/>
		<br/>
		确认密码：	<input type = "password" id = "3" name = "pawd" required="required"/>
		<br/>
		性       别：	<select name = "sex">
			<option>男</option>
			<option>女</option>
		</select>
		<br />
		年       龄：       <input type = "number" name = "age" />
		
		<bt />
		邮       件：       <input type = "email" name = "email" required="required"/>

		<input type = "submit"  onclick = "judge()" value = "注册"/>                                        <input type = "reset"  onclick = "rese()" />
		</form>
	</div>
</body>
</html>
```

* 连接数据库进行插入操作

```php+HTML
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8" />
	<title></title>
	<style type="text/css">
		div{
			margin :0 auto;
			text-align : center;
			border : 1px solid;
			width : 700px;
		}
	</style>
</head>
<body>
	<?php
	header("Content-type: text/html;charset = utf-8");
		if(empty($_POST))
		{
			echo "NoInformation";
		}else
		{
			header("Content-type: text/html;charset = utf-8");
			$host = "localhost";
			$username = "root";
			$password = "li33092728li";
			$database = "test";
			$port = "13140";
			$conn = @new mysqli($host,$username,$password,$database,$port);
			}
			if($conn->connect_errno){
	?>
				<script type="text/javascript">
					alert("数据库连接错误");
				</script>
	<?php
			die($conn->connect_error);
			}
			$conn->query("set names utf8");
			$is = $conn->query("INSERT INTO `user`(`username`, `pwd`, `age`, `Gender`, `email`) VALUES ('$_POST[username]','$_POST[pawd]','$_POST[age]','$_POST[sex]','$_POST[email]')");
	?>
	<div>
	<?php
			if($is)
			{
				echo("<h2>注册成功!</h2><br/>注册的数据如下：<br /><br />");

				echo("username:".$_POST["username"]."<br /><br />");

				echo("age:".$_POST["age"]."<br /><br />");

				echo("sex:".$_POST["sex"]."<br /><br />");

				echo("email:".$_POST["email"]."<br /><br />");

				$id = $conn->query("select last_insert_id()");

				$row = $id->fetch_row();
				echo("您的ID号为：".$row[0]."<br /><br />请记住此ID号，以便下次登录");
			}else
			{
				echo("<br/>注册失败");
			}
	?>
	</div>
</body>
</html>
```



# php获得数据源中的数据条数，返回int型

```php+HTML
mysqli_num_rows(数据资源);//面向过程写法
mysqli->num_rows()//面向对象写法
```

# php关闭数据库

```php+html
mysql_close(数据资源);
```

# php删除数据库内容

* 再query()语句中执行delete语句即可

# php查询数据库内容

```php+html
<!DOCTYPE html>
<html>
<head>
	<title></title>
</head>
<body>
	<?php
		$mysqli = new mysqli('localhost','my_user','my_password','my_db');
		$mysqli = new mysqli(数据库地址，用户名，密码，数据库名);
    	$sql = "select * from `user`";
    	$result = $conn->query($sql);
    	$row = $result -> fetch_row();
    	var_dump($row);
    	echo "id:".$row[0];
    	while($row = $result->fetch_row()){
            echo "id:".row[0]; //显示所有行
        }
	?>
</body>
</html>
```

# php返回刚刚自增创建的id

* 三种方法

* 用以下语句

  ```php+HTML
  $id = $conn->query("select max(id) from user");
  ```

  > 但是这种方法不适合多线程

* 用以下函数

  ```php+HTML
  $id = mysql_insert_id();
  ```

  > 当系统执行完INSERT后，再执行SELECT时，可能已经被分发到了不同的后端服务器，如果你使用的编程语言是PHP的话，此时应该通过 mysql_insert_id()来得到最新插入的id，每次INSERT结束后，其实对应的autoincrement值就已经计算好返回给PHP 了，你无需再发出一次独立的查询，直接用mysql_insert_id()就可以了这个函数很好用 当我们插入一条语句时 它自动返回了 最后的id值并且此函数 仅对当前链接有用 也就是说 它是多用户安全型的所以我们经常用此函数；
  >
  > 但此函数有一个问题 就是 当id 为bigint 型时 就不在起作用了 所以 现在 正在用此函数的请小心了不过 我们平时很少遇到这样的问题，所以可以不用管它。
  >
  > 但是我的用不了，字符集有问题

* 用以下查询

  ```php+HTML
  $result = $conn->query("select last_insert_id()");
  $id = $result->fetch_row();
  echo($id[0]);
  ```

  > 这个查询等同于第二种方法，而且解决了bigint的问题
  >
  > 这个我这里可以使用，没有字符集的问题