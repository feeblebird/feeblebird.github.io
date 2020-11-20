---
title: phpStudy
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

* print和echo的区别

  print使用方法与echo相同，不同的地方是print有返回值，返回值始终为1。

  所以使用过程中echo比print稍快，因为没有返回值

* print_r和var_dump的区别

  print_r输出数组

  var_dump输出数据类型和变量的值

 * echo 和 print 打印不出boolean的"true"和"false"

    true会打印出1,false会被认为是空

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

  * 含有单引号的话，就只是被认为是字符串

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
$b = array(
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

## 输出二维数组元素中的问题

```php+HTML
$a = "地支";
$c = 0;
echo "$b[$a][$c]";//不能得到我们想要的结果
```

> 这里的解决方法就和下面这个数组下标问题一样

```php+HTML
$a = '地支'; //这里**为单引号**
$c = 0;
echo "{$b[$a][$c]}";
echo $b[$a][$c];

$a = 地支;
$c = 0;
echo "{$b[$a][$c]}";//地支被解析为常量，若没有定义这个常量则会报错
echo $b[$a][$c];//地支被当作常量来处理，若没有定义这个常量则当作字符串处理
```

> 注意二维数组不能直接通过`echo "$b[name][name2]"; ` 输出的。
>
> 会报错，而一维数组可以

# 数组下标问题

* 数组的下标是不加引号、还是使用单引号、还是使用双引号

  * 不加引号：如果是数字下标就可，如果是字符串下标则还需要类型转换，影响效率
  * 加单引号：就是字符串
  * 加双引号：还要判断有无变量以及特殊字符转义，比单引号效率低一些

  ## 在双引号中有数组元素的访问时

  * [参考](https://blog.csdn.net/u012143455/article/details/50516965)

  * 当在双引号中有数组元素的访问的时候，如下的写法是 **错误** 的

    ```php+HTML
    echo "$_GET['name']";
    echo "$myarr['one']";
    ```

  * **正确做法** 如下，有三种：

    * 第一种：索引字符串不加引号

      ```php+HTML
      echo "$_GET[name]";
      ```

    * 第二种：索引字符串不加引号，且数组元素用花括号括起来

      ```php+HTML
      define ('name','age');
      echo "{$_GET[name]}";
      ```

      > 此时用花括号括起来的数组元素中的name就会被当作字符常量来处理，所以实际输出的相当于echo "$_GET[age]";
      >
      > 如果没有定义该常量，则会 **报错** 

    * 第三种：索引字符串加单引号，且数组元素用花括号括起来

      ```php+HTML
      echo "{$_GET('name')}";
      ```

      > 效果和第一种方法相同

  ## 数组元素下标是否加单引号(未使用双引号)

  * 加单引号

    ```php+HTML
    echo $_GET['name']; ==>echo $_GET["name"];
    ```

    > 即输出该输出的内容，name当作字符串处理

  * 未加单引号

    ```php+HTML
    echo $_GET[name];
    ```

    > 此时name被当作常量处理，如果没有定义常量name则当作字符串处理。即name不是常量时就和echo $_GET['name']效果相同。

  ## 数组元素下标是否加单引号和花括号(使用双引号)

  * 不加单引号，不加花括号

    ```php+HTML
    echo "$_GET[name]";
    ```

    > name被当作字符串处理，即输出我们想要的内容

  * 加花括号，不加单引号

    ```php+HTML
    echo "{$_GET[name]}";
    ```

    > name被当作字符常量处理，如果没有定义该常量，则会 **报错** 。

  * 加花括号，加单引号

    ```php+HTML
    echo "{$_GET['name']}";
    ```

    > name被当作字符串处理
  
  ## 数组下标被当作常量的情况
  
  * ```php+HTML
    echo "{$myarr[name]}";
    ```
  
    > 若常量不存在则会报错
  
  * ```php+HTML
    echo $myarr[name];
    ```
  
    > 若常量不存在则会将name解析成字符串
  
  ## 双引号中使用单引号
  
  ```php+HTML
  echo "'$myarr[name]'";
  相当于echo "'"."$myarr[name]"."'";
  ```
  
  > 但是
  
  ```php+HTML
  二维数组中就不能这样用
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

* shuffle();函数，将数组 **随机排序** 

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

* 两个函数对于错误处理( **主要区别** )
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

  * > **通过表单传递的参数是放在url(放在报文头)中，会覆盖原来url中的参数**

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
     		//或者  $_GET[username] $_GET["username"]
      	//或者  "{$_GET['username']}" 
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

  > php双引号中的单引号会被当作单纯的单引号，所以会吧变量转化为对应的值，此时转化完之后这些值都被单引号括起来，成为了sql中的字符串。

* 表单传递用_POST数组，信息不会出现在地址栏中

  > 表单的信息不会出现在地址栏(放在报文体中)中，所以不会覆盖url中原来的参数
  >
  > 所以可以在method=post中在url中加参数，统一也就get数组中传递了参数
  
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

# get方法传递参数，post方法传递参数，get和post方法一起传递参数

* get方法传递的表单的参数会放在url中(放在报文头中)，且表单的参数会覆盖原来的参数
* post方法传递的表单的参数不再url中(在报文体中)，且原来url中的参数不会被覆盖
* 所以可以在post方法中在url中加上参数，也通过get数组传递了参数。

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
推荐使用document.getElementById();
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
		<meta charset="utf-8" /> --客户端的编码方式
	</head>
	<body>
        <?php
        	header("Content-type: text/html;charset = utf-8");
        	//设置页面内容为html，变法方式为utf-8
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
       	//相当于
        //set character_set_client = 'utf8'
        //set character_set_connection = 'utf8'
        //set character_set_results = 'utf8'
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

* 返回值为资源类型的结果集
* 处理有效资源类型数据，返回数组类型
  * fetch_row() //获取结果集中的一行记录，返回索引数组(下标为1,2,3,4..)，取到一行后下标增一,即可以用一个循环输出所有行
  * fetch_array()//返回索引和关联数组，即返回下标(0,1,2,...)也返回数据库字段为下标
  * fetch_assoc()//直接返回以数据库字段为下标的数组

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

# sql语句中value中变量应该加' '

* 双引号中使用单引号

# header(locatoin:xxx.php)

* 执行跳转

# 实例:实现评论功能，可以修改，删除。

# die语句

* 停止后面的语句运行并输出语句

# fetch_row() fetch_assoc()

* `$result = $conn->query($sql)` 返回值为一个资源型结果集

* `$row = $result->fetch_row()` 将结果集中的下标对应的行取出来给$row

  没取出一个下标加一，所以可以用一个循环取出结果集中的所有行

* `$row = $result->fetch_assoc()`  一样的只是取出来的下标不同，区别如下：

  * fetch_row() //获取结果集中的一行记录，返回索引数组(下标为0,1,2,3,4..)，取到一行后下标增一,即可以用一个循环输出所有行
  * fetch_array()//返回索引和关联数组，即返回下标(0,1,2,...)也返回数据库字段为下标
  * fetch_assoc()//直接返回以数据库字段为下标的数组

# 分页技术

* 首页   上一页   下一页   尾页

* 首页:show.php?page=1

* 上一页:show.php?page =n-1(当前页为n)

* 下一页:show.php?page=n+1

* 尾页:show.php?page= 总页数

* 总页数=ceil(总记录条数/每页显示记录)

* ceil()函数：小数点舍掉并加一

* 从指定位置开始查询指定条数的记录

  ```sql
  select * from message limit sart,rows
  --start:起始位置(默认值为0)
  --rows:每次取几条记录
  第一页:select * from message limit 0,3
  第二页:select * from message limit 3,3
  第三页:select * from message limit 6,3
  ...
  第n页:select * from message limit 3*(n-1),3
  
  每页显示条数:$pagesize
  总页数:$totalPage = ceil(总记录条数/$pagesize)
  当前页码:$page
  select * from message limit ($page-1)*$pagesize,$pagesize
  ```

# 一个php文件中的多个php代码块

* 相当于一个代码块，然后代码进行合并

# php实现评论功能

* conn.php

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		header("Content-type: text/html;charset = utf-8");
  		$ip = 'localhost';
  		$user = 'root';
  		$password = 'li33092728li';
  		$database = 'test';
  		$port = '13140';
  		$conn = @new mysqli($ip,$user,$password,$database,$port);
  		if($conn->connect_errno)
  		{
  			die("数据库连接错误".$conn->connect_error);
  		}
  		$conn->query("set names utf8");	 
  	?>
  </body>
  </html>
  ```

* show.php

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf-8" />
  	<title></title>
  	<style type="text/css">
  		a{
  				text-decoration: none;
  		}
  		.mya{
  				text-decoration:underline;
  		}
  		textarea{
  			resize:none;
  			border:0;
  			border-radius:18px;
  			background-color:rgba(241,241,241,.98);
  			width: 355px;
  			height: 100px;
  			padding: 10px;
  		}
  	</style>
  	<script type="text/javascript">
  		function judge()
  		{
  			var name = document.getElementById("name2");
  			var title = document.getElementById("title2");
  			if(name.value == "")
  			{
  				name.value = "匿名用户";
  			}
  			if(title.value == "")
  			{
  				title.value = "无标题";
  			}
  		}
  		function do_del(id)
  		{
  			if(window.confirm('确定要删除吗'))
  			{
  				window.location.href = "delete.php?id="+id;
  			}
  		}
  	</script>
  </head>
  </head>
  <body>
  	<form style = "white-space:pre" action = "show.php" method = "post">
  		昵称:<input type = "text" placeholder = "请输入你的昵称" name = "name1" id = "name2" />
  
  		标题:<input type = "text" placeholder = "请输入标题" name = "title1" id = "title2" />
  
  		<textarea name = "content" placeholder = "留下些什么，证明你来过" required="required" ></textarea>
  
  		<input type = "submit" name = "sub" onclick="judge()" />
  	</form>
  	<?php
  		header("Content-type: text/html;charset = utf-8");
  		if(!empty($_POST))
  		{
  			require "conn.php";
  			$sql = "INSERT INTO `message`(`ID`,`Title`, `Author`, `Content`, `IP`, `Ptime`) VALUES (null,'$_POST[title1]','$_POST[name1]','$_POST[content]','$_SERVER[REMOTE_ADDR]',now())";
  			$is = $conn->query($sql);
  			if(!$is)
  			{
  				echo "插入失败";
  			}
  			header("location:show.php");
  		}
  	?>
  	<form method="get" action="">
  		<input type="text" name="key" /><input type="submit" name="sub" />
  	</form>
  	<?php
  		header("Content-type:text/html;charset=utf-8");
  		require "conn.php";
  		if(!empty($_GET['key']))
  		{
  			$key = $_GET['key'];
  			$k = "`Title` like '%$key%'";
  		}else
  		{
  			$k = "1";
  			$key = "";//不加这句如果url参数中没有key则没有这个变量，会出错
  		}
  		$pagesize = 3;
  		$sql = "select * from message where $k";
  		$result = $conn->query($sql);
  		$rows = $result->num_rows;//取出记录的总条数
  		//num_rows是结果集的属性，所以不加括号
  		$totalpage = ceil($rows/$pagesize);
  		if(!empty($_GET['page']))
  		{
  			$page = $_GET['page'];
  		}else
  		{
  			$page = 1;
  		}
  		$start=($page-1)*$pagesize;
  		$sql = "select * from `message` where $k order by `Ptime` DESC limit $start,$pagesize";
  		$result = $conn->query($sql);
  		while($row = $result->fetch_assoc())
  		{
  	?>
  			<hr />
  			<h3>标题：<?php echo $row['Title']; ?></h3>
  			<p>昵称：<?php echo $row['Author']; ?> | from: <?php echo $row['IP']; ?></p>
  			<p>留言内容(<?php echo $row['Ptime']; ?>)：<br />
  			<?php echo $row['Content']; ?></p>
  			<p>
  			<a href = edit.php?id=<?php echo $row['ID']; ?>>编辑</a> | <a href = "javascript:do_del(<?php echo $row['ID']; ?>)">删除</a>
  			</p>
  	<?php
  		}
  	?>
  	<p>
  	<?php
  		if($page>1)
  		{
  			echo '<a href = "show.php?page=1&key='.$key.'">首页</a> ';
  			echo '<a href = "show.php?page='.($page-1).'&key='.$key.'">上一页</a>';
  		}
  		for($i = 1;$i <= $totalpage;$i ++)
  		{
  			if($page!=$i)
  			{
  				echo '<a class="mya" href="show.php?page='.$i.'&key='.$key.'" >'.$i."</a>|";
  			}else
  			{
  				echo "$i|";		
  			}
  		}
  		if($page<$totalpage)
  		{
  			echo '<a href = "show.php?page='.($page+1).'&key='.$key.'">下一页</a> ';
  			echo '<a href = "show.php?page='.$totalpage.'&key='.$key.'">尾页</a>';
  		}
  	?>
  	</p>
  </body>
  </html>
  ```

* edit.php

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<meta charset = "utf8" />
  	<title></title>
  	<script type="text/javascript">
  		function judge()
  		{
  			var name = document.getElementById("name2");
  			var title = document.getElementById("title2");
  			if(name.value == "")
  			{
  				name.value = "匿名用户";
  			}
  			if(title.value == "")
  			{
  				title.value = "无标题";
  			}
  		}
  	</script>
  	<style type="text/css">
  		textarea{
  			resize:none;
  			border:0;
  			border-radius:18px;
  			background-color:rgba(241,241,241,.98);
  			width: 355px;
  			height: 100px;
  			padding: 10px;
  		}
  	</style>
  </head>
  <body>
  	<?php 
  		if(!empty($_GET))
  		{
  			require "conn.php";
  			$id = $_GET['id'];
  			$sql = "select * from `message` where `ID` = $id";
  			$result = $conn->query($sql);
  			$row = $result->fetch_assoc();
  			$title = $row['Title'];
  			$name = $row['Author'];
  			$content = $row['Content'];
  		}
  	?>
  	<form style = "white-space:pre" action = "edit.php" method = "post">
  		昵称:<input type = "text" placeholder = "请输入你的昵称" name = "name1" id = "name2" value = <?php echo '"'.$name.'"'; ?> />
  
  		标题:<input type = "text" placeholder = "请输入标题" name = "title1" id = "title2" value = <?php echo '"'.$title.'"'; ?> />
  
  		<textarea name = "content" placeholder = "留下些什么，证明你来过" required="required" ><?php echo $content; ?> </textarea>
  
  		<input type = "hidden" name = "id" value = <?php echo $id; ?> />
  
  		<input type = "submit" name = "sub" onclick="judge()" />
  	</form>
  	<?php
  		header("Content-type: text/html;charset = utf-8");
  		if(!empty($_POST))
  		{
  			require "conn.php";
  			$sql = "UPDATE `message` SET `Title`='$_POST[title1]',`Author`='$_POST[name1]',`Content`='$_POST[content]',`Ptime`=now() WHERE `ID` = $_POST[id]";
  			$conn->query($sql);
  			header("location:show.php");
  		}
  	?>
  </body>
  </html>
  ```

* delete.php

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  	
  </head>
  <body>
  	<?php 
  		if(!empty($_GET))
  		{
  			require "conn.php";
  			$id = $_GET['id'];
  			$sql = "delete from `message` where `ID` = $id";
  			$is = $conn->query($sql);
  		}
  		header("location:show.php");
  	?>
  </body>
  </html>
  ```

# php会话控制(cookie&session)

* 会话控制是为了解决什么问题

  http为无状态协议，为了让服务器跟踪同一个客户端发出的连续请求，而使用会话控制

* 绘画控制用到哪两种技术

  * 将用户状态信息，存放在客户端上，cookie
    * cookie是一种由服务器发送给客户端的片段信息，存储在客户端浏览器的内存或者硬盘上。
    * 常用于保存用户名，密码，个性化设置，个人偏好记录等
    * 当用户访问服务器时，服务器可以设置和访问cookie的信息
    * cookie存放的位置取决于浏览器
  * 将用户状态信息，存放再服务器中，session
    * 

* 这两种技术有什么特点

# cookie

* 设置cookie

  ```php
  setcookie("username","sky",time()+60*60*24*7);
  //向客户端发送一个Cookie，将变量username值为sky，保存一周时间
  //直接写数字，以秒为单位，不行
  //以time()为基准
  //不设置存在时间，则只会存放在客户端内存中，当关闭会话后，不会存储在客户端上
  ```

* 访问$_COOKIE

  ```php+HTML
  <!DOCTYPE html>
  <html>
  <head>
  	<title></title>
  </head>
  <body>
  	<?php
  		setcookie("testcookie","My first cookie",time()+24*60*60*30);
  		setcookie("username","admin111",time()+60*60*24*7);
  		print_r($_COOKIE);
  		if(isset($_COOKIE['username']))
  		{
  			echo "欢迎回家";
  			echo $_COOKIE['username']."来访<br/>";
  		}else
  		{
  			echo "欢迎你首次访问本网站";
  		}
  	?>
  </body>
  </html>
  ```

* 修改username的值时，第一次刷新不改变，第二次刷新才改变

  因为第一次刷新的时候，执行setcookie语句，将设置内容发送给服务器，但是我们本地还没有被服务器写入，后面访问本地cookie时还是原来的值，第二次刷新的时候服务器写入了，所以本地cookie也更新了。

* 删除cookie

  * 忽略setcookie参数，只指定第一个参数

    ```php
    setcookie("username");
    ```

  * 设置已经过期

    ```php
    setcookie("username","",time()-1);
    ```

# session

* session把cookie存放在服务器信息上

* 客户端上只需要一个唯一的session id，session id往往以cookie的形式存放在客户端上

* 如果客户端禁止cookie，则可以通过attach在url上的方式

* 使用方式

  * ```php
    session_start();
    //一般写在最前面
    ```

  * 直接以数组的方式使用

  * ```php
    unset($_SESSION['key']);
    //删除某个key值对
    session_destory();
    //销毁整个session
    ```

  * 