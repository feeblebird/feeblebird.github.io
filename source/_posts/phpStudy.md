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
  	?>
  </body>
  </html>
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

  