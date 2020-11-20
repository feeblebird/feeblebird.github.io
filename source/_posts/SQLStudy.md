---
title: SQLStudy
date: 2020-09-19 19:09:02
tags: SQL
categories: SQL
---

# SQL不区分大小写

> sql是大小写无关的，他把大写和小写字母看作相同的字母。举个例子，对于保留字FROM，无论写成FROM、From或者FrOm都是正确的。
>
> 关系名、属性名和别名都同样是大小写无关的。
>
> 只有引号里面的字符才是区分大小写的。

# 语法

* #### 进入mysql(dos窗口中)

  ```sql
  mysql -h localhost -u root -p password
  //-h 为ip地址,本机为localhost或者127.0.0.1
  //-u 为user用户名
  //-p 小写，后面为密码 或者 不输入，因为不做隐藏的
  //-P 为Port端口号
  ```

* #### help命令

  使用help查看一些命令，这些命令在使用的时候都不用加分号。

* #### 数据库管理

  ```sql
  show databases;
  create database dbname;
  drop database dbname;
  ```

* #### 使用某一个数据库

  ```sql
  use database dbname;
  ```

* #### 数据表管理

  ```sql
  show tables;
  create table tbname;
  drop table tbname;
  ```

* #### sql数据类型

  ```sql
  tinyint         1byte
  smallint		2byte
  mediumint		3byte
  int/integer		4byte
  bigint			8byte
  float			4byte
  double			8byte
  decimal			
  -----------------------------
  date		3byte 1000-01-01/9999-12-31
  time 		3byte -839:59:59/839:59:59
  year		1byte 1901/2155
  datetime 	8byte 1000-01-01 00:00:00/9999-12-31 23:59:59
  timestamp	4byte 0/2147483647(时间戳)
  //以字符串的形式'2020-01-01 15:30:02.5'
  -----------------------------
  char		定长字符 					0-255byte
  varchar		变长字符 					0-65535byte
  tinyblob	二进制字符串 				   0-255byte
  tinytext	短文本字符串				   0-255byte
  blob		二进制形式长文本数据 			0-65535byte
  text		长文本数据 					0-65535byte
  mediumblob	二进制形式的中等长度文本数据	  0-16777215byte
  mediumtext	中等长度文本数据			  0-16777215byte
  longblob	二进制形式的极大文本数据	   0-4294967295byte
  longtext	极大文本数据				   0-4294967295byte
  ```

* #### 约束类型

  ```sql
  not null 用于限制该字段为必填项
  default 用于限制该字段没有显式插入值，则直接显示默认值
  primary key  用于限制该字段值不能重复，设置为主键列的字段默认不能为空，可以联合主键，但一个表只能有一个主键
  unique 用于限制该字段不能重复，字段可以为空，一个表可以有多个unique
  check  用于限制该字段值必须满足指定条件
         check(age between 1 and 100)
  foreign key 外键：用于限制两个表的关系，要求外键列的值必须来自主表的关联列
  		要求：
  		①主表的关联列和从表的关联列的类型必须一致，意思一样，名称无要求
  		②主表的关联列要求必须是主键
  ```
  
  
  
* #### 创建数据表

  ```sql
  create table tbname(
  	attribute1 varchar(20)/char(20),
      attribute2 integer/int/smallint,
      attribute3 date,
      attribute4 time,
      attribute5 real/float,
      attribute6 real/float default 0.1 //设置默认值为0.1
  );
  create table tbname(
  	attribute1 varchar(20)/char(20) not null,
      attribute2 integer primary key//主键 默认不能为空
      //attribute2 integer unique //逐渐 可以为空
  );
  create table tbname(
  	attribute1 varchar(20) not null,
      attribute2 real not null,
      primary key(attribute1,attribute2)//联合主键 默认不能为空
  );
  create table tbname(
  	attribute1 varchar(20) not null,
      attribute2 float not null,
      unique(attribute1,attribute2)//联合主键 默认可以为空
  );
  ```


* #### unique约束和primary key约束

  * 在一个表中只能有一个primary key但是可以多个unique
  * primary key 和 unique 约束都能约束某个属性值不能重复，primary key 约束的属性值不能为空，unique 约束的属性可以为空。

* #### 插入数据

  ```sql
  insert into tbname //这里不能加table，不然执行不了
  (attribute1,attribute2,attribute3...)
  valuses
  (value1,value2,value3...)
  ```

* #### 修改表(最好在加入数据前修改表)

  ```sql
  alter table tbname
  add|modify|change|drop column 字段名 字符类型 字段约束;
  ```

  ```sql
    alter table tbname
    rename to newtbname; --改表名
  ```

  ```sql
    alter table tbname
    add column bir datetime not null; --添加属性
  ```

  ```sql
    alter table tbname
    change column bir birthday datetime; --修改属性名，类型必须要加，可以认为这里的修改就是删除原来的属性而添加一个新的属性，约束也可以改变。  
  ```

  ```sql
    alter table tbname
    modify column bir timestamp; --修改属性类型
    
    alter table tbname
    modify column bir timestamp not null;
    --可以修改属性从空变为不空，或反之，相当于重新设置了一个属性
  ```

  ```sql
    alter table tbname
    drop column bir; --删除属性
  ```

  ```sql
    alter table tbname
    drop primary key; --删除主键
  ```

  ```sql
    alter table tbname
    change column bir bir datetime unique;--添加约束
    change column bir bir datetime primary key;--如果此时该属性的值为not null则可以，否则应该先设置为not null,因为primary key默认not null
    
    alter table tbname
    modify column bir bir datetime primary key; --若非空则可以设置称主键
  ```

* #### 删除表

  ```sql
  drop table if exists tbname;
  ```

* #### 复制表

  ```sql
  create table newtable like oldtable;
  //只是赋值表结构
  create table newtable select * from oldtable;
  //复制本库另一个表的内容
  create table newtable select * from girls.'beauty';
  //复制别的库里面的内容，girls库里面的beauty表
  create table newtable select last_name,department_id from myemployee.'employees' where 1=2;
  //只复制myemployee库中的employees表中的last_name,department字段的结构，不包括具体数据
  ```


# select from where 语句

```sql
SELECT *
FROM drinkers
WHERE trim(NAME) LIKE '% % %';
--去掉前后的空格，中间的空格不去,选出名字由三部分组成
```

# AS 关键字

* #### 给关系起别名

  ```sql
  //给关系起别名，可认为原来是原名 as 原名
  SELECT bar,beer
  from bars [as] ba,beers [as] be //as可省略    
  where ba....   be....;
  ```

* #### 给属性起别名

  ```sql
  //给属性起别名
  SELECT bar,beer,price as priceInYen
  from sells;
  ```

* #### 属性可以被表达式替代

  ```sql
  //属性可以被表达式替代
  SELECT bar,beer,price*14 as priceInYen
  from sells;
  ```
  
* #### 将常量作为表达式在SELECT语句中列出

  ```sql
  SELECT title,length,'hrs.' AS inHours
  from movies
  where studioname = 'Disney' AND year = 1990;
  
  //则结果中会出现一列属性名为inHours的列，值都为'hrs.'
  ```

  > 可以理解为查询时，每次都是将关系中的元组赋值给select-from-where语句中的select中的属性，然后判断条件是否满足，所以那个常量就一直是这个而且保留了下来。

# where语句中的运算符

* #### 算术运算符

   有+ - * /

* #### 字符串连接符

  ```sql
  'foo'||'bar'相当于'foobar'
  ```

* #### 比较运算符

  ```sql
  >
  <
  >=
  <=
  =
  <>
  ```

* #### 逻辑运算符

  ```sql
  AND
  OR
  NOT
  //可以对返回值为布尔值的表达式进行取非
  ```
# 单引号中使用单引号

```sql
'i''m liwei' => i'm liwei
```

# NULL

* 与其他进行运算值都是NULL

* 与其他值比较结果为unknow

* 判断是否为空

  where is now; / where is not null;

# 字符串比较

* #### 注意这里进行字符串比较的时候会忽略SQL为了保证字符串长度而填充的填充字符，而SQL串的模式匹配中不会忽略。

* #### 在SQL模式匹配中使用trim函数取出字符串两端的空格。

# 字符串模式匹配

```sql
S LIKE P
S NOT LIKE P
```

* S是字符串

* P是模式(pattern)

* #### 模式匹配中的特殊字符

  * %，能匹配任意长度的串
  * _ ，能匹配s中任何一个字符

* #### 模式匹配中使用%和_，使用转义字符

  > like表达式中的转移字符
  >
  > like表达式中没有固定的转移字符，而是通过 escape关键字指定转义字符。
  >
  > 比如：WHERE beer LIKE 'x%x%' ESCAPE 'x';就是指定x为转义字符。

# 输出排序

```sql
ORDER BY <list of attributes>
select *
from movies
where studioName = 'Disney' AND year = 1990
ORDER BY length,title ASC;
//ORDER BY length,title DESC;
```

* #### ASC DESC指定是升序还是降序

* #### ORDER语句后面也可以是表达式

```sql
SELECT *
FROM R
ORDER BY A+B DESC;
```


# 多表查询，多关系查询

```sql
SELECT l1.drinker
FROM likes l1,likes l2,likes l3
WHERE l1.drinker = l2.drinker AND l1.drinker = l3.drinker
AND l1.beer < l2.beer AND l2.beer < l3.beer;
```

# 元组变量

* #### 通俗来讲就是给关系起个别名

* #### 在一个select-from-where语句中，要将同一个关系中的不同元组进行比较的时候

  ```sql
  select *
  from likes l1,likes l2
  where l1.name = l2.name and l1.beer <> l2.beer;
  ```

# 查询的结果是一个Bag，即没有不重复性

* #### 但是当进行查询的并、交、差的时候会先去重，转换成一个集合，因为这样效率高。

* 理论上的方法是先对两个查询结果进行一个排序，然后遍历一遍去重，然后在遍历进行集合运算。

# Controlling Duplicate Elimination控制重复消除

* #### 强+/制去重

  ```sql
  select distinct price
  from sells;
  ```

* #### 强制将集合转换为Bag(在子查询关系运算中使用ALL关键字)

  ```sql
  (select drinker from frequents)
  union all
  (select drinker from likes);
  
  (select drinker from frequents)
  intersect all
  (select drinker from likes);
  
  (select drinker from frequents)
  except all
  (select drinker from likes);
  ```

# 查询的并、交、差

* #### intersect 交

* #### union 并

* #### except 差

  >  这三个运算都是查询结果与查询结果之间进行的。两个subquery用小括号括起来，中间用这三个运算符连接。

# 使用子查询(subquery)的情况

* #### 出现在from中

  > 若出现在from中则在子查询后面应该紧跟该子查询结果对应的元组变量(tuple variable)

  ```sql
  select likes.name
  from (slect * from bars) B,likes
  where B.beer = likes.beer and b.bar = likes.bar;
  ```

* #### 出现在where中

  * 若子查询结果为一个元组，则这个元组的具体属性值就可以用来进行比较
  * 若子查询结果为一个关系，则可以在where以不同的方式使用，就和普通的关系类似。

# 关系的条件表达式(值与关系之间)

* #### EXISTS

  * EXISTS R 若R不为空，则该值为true，反之为假
  * NOT EXISTS R

* #### IN

  * IN R
  * NOT IN R

* #### ANY

  * s > ANY R
  * NOT s > ANY R

* #### ALL

  * s > ALL R
  * NOT s > ALL R

# 元组的条件表达式(元组与关系之间)

* #### 如果元组与该关系的元组之间有相同的组成分量(component)个数，那么这个比较是有意义的

```sql
select name
from MovieExec
where cert# IN
(select producerC#
from Movies
where (title,year) IN
 	(select movieTitle,movieYear
    from StarsIn
     Where starName = 'Harrison Ford'
    )
);
```

# 关联子查询，相关子查询(correlated subquery)

* #### 在子查询过程中要用到子查询外部关系的元组

  ```sql
  select title 
  from movies Old
  where year < any
  (
  	select year
      from movies
      where title = Old.title
  );
  ```

  > 属性名子的作用范围，即就近原则，近的找不到关系中有该属性，则去远处找

# SQL连接表达式

# cross join 笛卡尔乘积

```sql
select *
from likes cross join sells;
```

> 列数相加，行数相乘

# 自然连接Natural Join

```sql
select likes.beer,drinker,bar,price
from likes,sells
where likes.beer = sells.beer;
//先是做一个笛卡尔乘积，然后两个表中相同的属性值相同的元组成为连接结果，且同名属性值相同的合并。
//下面这三种写法是等价的，只是nutural join结果会合并属性列
SELECT *
FROM likes NATURAL JOIN sells;
SELECT *
FROM likes JOIN sells ON likes.beer = sells.beer;
SELECT *
FROM likes CROSS JOIN sells
WHERE likes.beer = sells.beer;
```

> 先做一个 **笛卡尔乘积** 
>
> 如果有多个同名的属性，则保留下来的成为结果的元组中的这些属性值都要相同。
>
> **且进行了合并**

# Theta Join

```sql
select *
from drinkers [inner] join frequents on name = drinker
[where ...]
;
//就是先做笛卡尔成绩，然后根据这个条件筛选,还可以继续根where
//相当于与
select *
from drinkers,frequents
where name = drinker;
```

# XXX Outer joins

> 注意outer join 是针对前面的natural join 和 join on的
>
> 所以分为

```sql
natural left outer join
natural right outer join
natural full outer join

left outer join on
right outer join on
full outer join on
```
```sql
natural LEFT OUTER JOIN
//连接关键字左边的表中的所有的元组都会列出来，如果该元组不满足条件则列出NULL
natural RIGHT OUTER JOIN
natural FULL OUTER JOIN
```

* #### natural left outer join

  >  **包含nutural join的结果，如果查询结果中没有包含关键词左边的关系中的某个元素，则会把这个元素加入结果，没有和右边关系匹配上的属性值由NULL补全。**

* #### natural right outer join

  > **包含nutural join的结果，如果查询结果中没有包含关键词右边的关系中的某个元素，则会把这个元素加入结果，没有和左边关系匹配上的属性值由NULL补全。**

* #### natural full outer join

  > **包含nutural join的结果，如果查询结果中没有包含关键词左边或右边的关系中的某个元素，则会把这个元素加入结果，没有和右边或左边关系匹配上的属性值由NULL补全。**

> 如果A natural join B的结果中，A 和 B的同名属性为attribute1，则如果结果中包含A中attribute1(转换成set)的所有值，且包含B中attribute1(转换成set)的所有值，则上面三种outer join查询出来的结果都一样。

# 给关系起别名后不能再from这个别名

```sql
SELECT likes.drinker
FROM likes,(((select name from bars)UNION(select name from beers))UNION(select name from drinkers))R
WHERE likes.beer IN
(
	SELECT name
	FROM R
);
```

> 不能这样子

# 例题

* 找出具有相同口径火炮的船只中火炮数量最多的船只的名字

```sql
SELECT NAME
FROM Ships
WHERE CLASS IN
(
	SELECT CLASS
	FROM Classes c1
	WHERE numGuns >= ALL
	(
		SELECT numGuns
		FROM Classes c2
		WHERE c1.bore = c2.bore
	);
);

SELECT NAME
FROM Ships
WHERE CLASS = ANY
(
	SELECT class
	FROM Classes c1
	WHERE NOT exists
	(
		SELECT *
		FROM Classes c2
		WHERE c1.bore = c2.bore AND c1.numGuns < c2.numGuns
	)
);
```

# 习题

* 6.3.1

  * (1)

    ```sql
    SELECT maker
    FROM Product
    WHERE model IN
    (
    	SELECT model
    	FROM PC
    	WHERE speed >= 3
    );
    
    
    SELECT maker
    FROM Product,(SELECT * FROM PC WHERE speed >= 3) high
    WHERE Product.model = high.model;
    ```

  * (2)

    ```sql
    SELECT model
    FROM Printer
WHERE price >= ALL 
    (
    	SELECT price
    	FROM Printer
    );
    
    
    SELECT model
    FROM Printer l1
    WHERE NOT EXISTS
    (
    	SELECT *
    	FROM Printer l2
    	WHERE l2.price > l1.price
    );
    ```
    
  * (3)
  
    ```sql
    SELECT model
    FROM Laptop
    WHERE speed < ALL
    (
    	SELECT speed
    	FROM PC
    	WHERE speed <= All
    	(
    		SELECT speed
    		FROM PC
    	)
    );
    
    
    SELECT model
    FROM Laptop l1
    WHERE NOT EXISTS
    (
    	SELECT *
    	FROM PC
    	WHERE speed <= l1.speed
    );
    ```
  
  * (4)
  
    ```sql
    SELECT Product.model
    FROM Product
  WHERE model IN
    (
    	SELECT model
    	FROM (((select price from pc)UNION(select price from Laptop))UNION(select price from Printer)) R
    	WHERE price >= ALL
    	(
    		SELECT price
    		FROM (((select price from pc)UNION(select price from Laptop))UNION(select price from Printer))
    	)
    );
    
    
    SELECT Product.model
    FROM Product
    WHERE model IN
    (
    	SELECT model
    	FROM (pc NATURAL FULL OUTER JOIN Laptop)NATURAL FULL OUTER JOIN Printer
    	WHERE price >= ALL
    	(
    		SELECT price
    		FROM (pc NATURAL FULL OUTER JOIN Laptop)NATURAL FULL OUTER JOIN Printer
    	)
    );
    ```
    
  * （5）
  
    ```sql
    SELECT maker
    FROM product
    WHERE model IN
    (
    	SELECT model
    	FROM Printer
    	WHERE price <= all
    	(
    		SELECT price
    		FROM Printer
    	)
    );
    
    
    SELECT maker
    FROM product
    WHERE model=ANY
    (
    	SELECT model
    	FROM Printer p1
    	WHERE NOT exists
    	(
    		SELECT *
    		FROM Printer p2
    		WHERE p2.price < p1.price
    	)
    )
    ```
  
  * (6)
  
    ```sql
    SELECT maker
    FROM product
    WHERE model IN
    (
    	SELECT model
    	FROM PC
    	WHERE ram <= ALL(SELECT ram FROM PC) AND speed >= ALL(SELECT speed FROM PC)
    );
    
    
    SELECT maker
    FROM product
    WHERE model =ANY
    (
    	SELECT model
    	FROM PC p1
    	WHERE NOT EXISTS (SELECT ram FROM PC p2 WHERE p2.ram < p1.ram ) AND NOT EXISTS (SELECT speed FROM PC p2 WHERE p2.speed > p1.speed)
    );
    ```
  
* 习题6.3.2

  * (1)

    ```sql
    SELECT country
    FROM Classes
    WHERE numGuns >= ALL
    (
    	SELECT numGuns
    	FROM Classes
    );
    
    
    SELECT country
    FROM Classes c1
    WHERE NOT EXISTS 
    (
    	SELECT *
    	FROM Classes c2
    	WHERE c2.numGuns > c1.numGuns
    );
    ```

  * （2）

    ```sql
    SELECT DISTINCT CLASS
    FROM Ships
    WHERE NAME IN
    (
    	SELECT ship
    	FROM Outcomes
    	WHERE RESULT = sunk
    );
    
    
    SELECT DISTINCT CLASS
    FROM Ships s1
    WHERE NOT EXISTS
    (
    	SELECT *
    	FROM Outcomes o1
    	WHERE s1.ship = o1.name AND o1.result = 'ok'
    );
    ```

  * (3)

    ```sql
    SELECT NAME 
    FROM Ships
    WHERE CLASS IN
    (
    	SELECT class
    	FROM Classes
    	WHERE bore = 16
    );
    
    
    SELECT NAME
    FROM Ships s1
    WHERE NOT EXISTS
    (
    	SELECT *
    	FROM Classes c1
    	WHERE s1.class = c1.class AND c1.bore <> 16
    );
    ```

  * (4)

    ```sql
    SELECT DISTINCT battle
    FROM Outcomes
    WHERE ship IN
    (
    	SELECT name
    	FROM Ships
    	WHERE CLASS = 'Kongo'
    );
    
    SELECT DISTINCT battle
    FROM Outcomes o1
    WHERE EXISTS
    (
    	SELECT *
    	FROM Ships s1
    	WHERE o1.ship = s1.name AND CLASS = 'Kongo'
    );
    ```

  * (5)

    ```sql
    SELECT NAME
    FROM Ships
WHERE CLASS IN
    (
    	SELECT CLASS
    	FROM Classes c1
    	WHERE numGuns >= ALL
    	(
    		SELECT numGuns
    		FROM Classes c2
    		WHERE c1.bore = c2.bore
    	);
    );
    
    SELECT NAME
    FROM Ships
    WHERE CLASS = ANY
    (
    	SELECT class
    	FROM Classes c1
    	WHERE NOT exists
    	(
    		SELECT *
    		FROM Classes c2
    		WHERE c1.bore = c2.bore AND c1.numGuns < c2.numGuns
    	)
    );
    ```
    

# homework1

>  
>
>   **Homework**  
>
>   Consider the following schema:  
>
>   Supplier(sid: integer, sname: string, address: string)  
>
>   Part(pid: integer, pname: string, color: string)
>
>   Catalog(sid: integer, pid: integer, cost: real) 
>
>  The relation Supplier stores suppliers and the key of that relation is sid.
>
>  The relation Part  stores parts,  and pid is the key of that relation.
>
>  Finally, Catalog stores which  supplier  supplies which part at which cost.  The key is the combination of the two attributes sid  and pid.  
>
>   **Write queries in SQL.**  
>
> 1. Find the names of suppliers who supply  some red part.  
> 2.  Find the IDs  of suppliers who supply some  red part and some green part. 
> 3. Find pairs of IDs such that the supplier with the first ID charges more for some part  than the supplier  with the second ID.  
>4. Find the IDs  of suppliers who supply  only red parts.  
> 5.  Find the IDs  of suppliers who supply every part.  

* 1

  ```sql
  SELECT distinct s.sname
  FROM Supplier s,Catalog c,part p
  WHERE s.sid = c.sid AND p.pid = c.pid AND p.color = 'red';	
  
  
  SELECT distinct sname
  FROM Supplier
  WHERE sid IN
  (
  	SELECT sid
  	FROM Catalog 
  	WHERE pid IN
  	(
  		SELECT pid
  		FROM Part
  		WHERE color = 'red'
  	)
  );
  
  
  SELECT distinct sname
  FROM Supplier
  WHERE sid IN
  (
  	SELECT sid
  	FROM CATALOG c1
  	WHERE EXISTS 
  	(
  		SELECT *
  		FROM Part p1
  		WHERE p1.pid = c1.pid AND color = 'red'
  	)
  );
  
  
  SELECT distinct sname
  FROM ((Supplier NATURAL JOIN Catalog)NATURAL JOIN Part)n
  WHERE n.color = 'red';
  ```

* 2

  ```sql
  SELECT sid
  FROM Catalog
  WHERE pid IN (SELECT pid FROM Part WHERE color = 'red') AND pid IN (SELECT pid FROM Part WHERE color = 'green')
  
  
  (
  		SELECT c.sid FROM Catalog c,Part p WHERE c.pid = p.pid AND color = 'red'
  )
  INTERSECT
  (
  		SELECT c.sid FROM Catalog c,Part p WHERE c.pid = p.pid AND color = 'green'
  )
  
  
  SELECT distinct n1.sid
  FROM (Catalog NATURAL JOIN Part)n1 JOIN (Catalog NATURAL JOIN Part)n2 ON n1.sid = n2.sid
  WHERE n1.color = 'red' AND n2.color = 'green';
  ```

* 3

  ```sql
  SELECT c1.sid,c2.sid
  FROM Catalog c1,Catalog c2
WHERE c1.pid = c2.pid AND c1.sid <> c2.sid AND c1.cost > c2.pid;
  
  
  SELECT c1.sid,c2.sid
  FROM Catalog c1 JOIN Catalog c2 ON (c1.pid = c2.pid AND c1.sid <> c2.sid AND c1.cost > c2.cost);
  ```
  
* 4

  ```sql
  SELECT sid
  FROM Catalog c1
  WHERE NOT EXISTS
  (
  	SELECT *
  	FROM Part p1
  	WHERE p1.sid = c1.sid AND p1.color <> 'red'
  );
  
  
  SELECT sid
  FROM Supplier s1
  WHERE NOT EXISTS
  (
  	(Catalog NATURAL JOIN Part)n1 JOIN (Catalog NATURAL JOIN Part)n2 ON (s1.sid = n1.sid AND n1.sid = n2.sid AND (n1.color <> 'red' OR n2.color <> 'red'))
  );
  ```

* 5

  ```sql
  SELECT sid
  FROM Supplier s1
WHERE NOT EXISTS 
  (
  	(
  		SELECT pid
  		FROM Part
  	)
  	except
  	(
  		SELECT pid
  		FROM Catalog c1
  		WHERE c1.pid = s1.pid
  	)
  );
  ```

# SQL修改表中元组中元素

```sql
update tablename
set attribute1=value1,attribute2=value2,....
where 更新条件表达式;
```

# SQL删除表中元组

```sql
delete from tablename
where 删除条件表达式;
```
# 聚合函数（将多个值聚合成一个值）

```sql
sum(attribute) avg(attribute) count(attribute) min(attribute) max(attribute)
count()--不会数null
count(*) --查找的是元组的数量
```

# 若使用聚合函数，select中 其他属性要么使用聚合函数，要么使用group by   

* 错误代码

```sql
SELECT bar, MIN(price)
FROM Sells
WHERE beer = '喜力';
--这个代码是错误的
```

* 正确代码

```sql
SELECT bar, price FROM Sells
WHERE beer = '喜 力' 
AND price = ( 
	SELECT MIN(price) FROM Sells
	WHERE beer = '喜力');

```

# GROUP BY分组

* 对查询结果中的元组的性质有限制的话，在where语句中进行限制
* 对group by分组的整体的性质有限制的话，在group by语句后面加上having限制

* 分完组后select对每一组分别进行统计。

> 一个关系中任何一个属性使用了聚合函数，则其他属性要么也使用聚合函数，要么使用Group by

> 使用group by后，select的作用对象就成了**每个分组**

#  having 只能对分组整体进行限制

* 若出现having 则必须放在group by后面，对每个分组进行判断，将分组当成一个整体，不是一个一个元组判断。

# 聚合函数不能出现在where语句中

*  因为where中式 **一个一个元组 **带进去判断where条件的，但是聚合函数用到了整个属性

# 聚合函数和分组中的NULL值

* NULL对平均值、求和、最大值、最小值、计数都不做贡献
* 分组中对NULL值没有要求，可以出现NULL
* 如果对空包(只有null)计数，则为零，其他聚合运算结果为null

# 属性的默认值

```sql
create table tablename
(
	attribute1 type1 default defaultvalue
);
```

# 表的更新

* insert

  ```sql
  insert into likes(beer,drinker)
  values();
  ```

  > 忘记表中attribute的顺序，可以指定插入值对应的属性

  ```sql
  insert into drinkers(name)
  values();
  ```

  > 插入部分的值

  ```sql
  insert into tablename
  (
  	subquery
  )
  ```

  > 插入多个元组

* delete

  ```sql
  delete 
  from tablename
  where condition;
  ```

  ```sql
  DELETE *
  FROM Beers b
  WHERE EXISTS (
  			SELECT name FROM Beers
  			WHERE manf = b.manf AND
  			name <> b.name);
  ```

  > 删除时先给满足条件的元组进行标记，而不是边删边查

* update

  ```sql
  update tablename
  set attribute1 = value
  where conditions;
  ```

# (views)视图和(indexes)索引

* a view is a relation defined in terms of stored tables(called base tables) and other views

> 视图依赖于其它的表或者其它的视图，所以 必须要有表

* two kinds:

  * virtual = not stored in the database;(默认情况)

    just a query for constructing the relation

    >  不会创建表，一个表中有敏感信息，要提供有选择性的服务，这时候就能提供视图，通过视图进行部分信息展示。
    >
    > 对多个表的复杂查询定义成一个视图，然后之后的复杂查询可直接对这个视图进行查询

    ```sql
    --virtual
    create view <name> [attributes](为select选择的内容重命名，可省略，否则用query中的属性名)
    as
    	<query>;
    	
    --materialized
    create materialized view <viewname>[attributes]
    as 
    	<query>;
    ```

    ```sql
    create view CanDrink(drinker,beer)--没有指定属性，则用query中的drinker,beer属性
    as
    	select drinker,beer
    	from frequents,sells
    	where frequents.bar = sells.bar;
    ```

  * materialized(物化的) = actually constructed and stored

* 对视图的查询

  ```sql
  select beer 
  from CanDrink
  where drinker = 'Tony Hoare';
  
  --相当于
  select beer 
  from 
  (
  	select drinker,beer
  	from frequents,sells
  	where frequents.bar = sells.bar
  ) CanDrink
  where drinker = ' ';
  
  --系统优化成
  
  select beer
  from frequents,sells
  where frequents.bar = sells.bar and drinker = ' ';
  ```
  
* 对视图的修改

  > 类似于对视图的查询
  >
  > opengauss中禁止对视图的修改，因为视图的目的就是给客户进行信息的展示
  >
  > sqlserver中支持

  * 重命名视图

    ```sql
    rename view viewname1 to viewname2;--sql中
    ```

* 删除视图

  ```sql
  drop view viewname;
  ```

* 物化的视图

  > 物化的视图查询快，但是
  >
  > 如果数据源的表改变了，视图应该保持一致(阶段性更新)
  >
  > 但是如果表变化的频率太快，则不太适合

# SQL Tuning Advisor(STA)

* sql自动优化

# 索引

* 加速数据的访问

  数据结构使用的是B-tree

* 创建索引

  ```sql
  --一个索引对应很多值
  create index indname on realtion(attribute);  
  create index indname on realtion(attribute1,attribute2,...);
  
  --一个索引对应一个值
  create unique index indname on relation(attribute);
  ```

* 索引使用

  * 只有当数据量很大的时候，定义索引后才会使用

    ```sql
    create index beerind on beers(manf);  
    create index sellind on sells(bar,beer);  
    
    select price
    from beers,sells
    where manf = 'pete''s'  --根据索引查找
    and beers.name = sells.beer --根据索引查找
    and bar = 'joe''s bar'; --根据索引查找
    ```

    > 运算符只能使用=

* 我们定义了索引后

  如果经常进行更新操作，索引会降低速率，因为更新后索引也要更新

* 如果不进行查询，则建立索引会降低效率

* 创建primary key或unique key后会自动创建索引，故我们要自己创建索引时要先把主键或者unique key删除掉

# 实体关系模型(Entity-Relation Model)

* 包含约束，不包含操作


# 实体集Entity

* 类似于面向对象中的类
* 包含简单的属性(属性不能是集合)

# 联系relationship(二元)

![image-20201103164015576.png](https://i.loli.net/2020/11/11/IOCKgjGbWM3ZLsD.png)

# 联系集(relationship set)

* 两个有联系的实体集的集合

# 多元联系(多路联系)(Multiway relationshiops)

![image-20201103164640201.png](https://i.loli.net/2020/11/11/KfivRtzYW1MCcAS.png)

# 多对多联系(many-many relationships)

* 联系关联的任一实体集中的一个实体可以对应其它实体集中的多个实体

  ![image.png](https://i.loli.net/2020/11/14/Z9WdYKRjqE1iFAI.png)

# 多对一联系(many-one relationships)

* 前一个实体集中的多个实体对应后一个实体集中的至多一个实体

* 后一个实体集中的一个实体对应前一个实体集中的零个、一个、多个实体

  ![image.png](https://i.loli.net/2020/11/14/f1FdX2KmrU5T4R3.png)

# 一对一联系(one-one relationships)

* 一对一

  ![image-20201114204101921](G:\typoraimages\image-20201114204101921.png)

# 联系的多样性(mltiplicity)

* 再E/R图中表示联系的多样性

* 多对多

  ![image-20201103165501064.png](https://i.loli.net/2020/11/11/tEYbOUDJGv78Zfi.png)

  或者在横线上加m,n

* 多对一

  ![image-20201103165522220.png](https://i.loli.net/2020/11/11/YV5isDBduEX4fKG.png)

  或者在横线上加m,1

  > 如果是尖尖的箭头，则每个人之多有一个最喜欢的啤酒，可以没有
  >
  > 可以为空
  >
  > 如果是圆的箭头，则每个人必须有一个最喜欢的啤酒
  >
  > not null

* 一对一

  ![image-20201103170031650.png](https://i.loli.net/2020/11/11/DHBsgyJhz5Zxe4C.png)

  > 该联系中，每个厂商必须有销售最好的啤酒，而啤酒不一定能对应上厂商
  >
  > 所以指向Beer的箭头是圆圆的箭头，表示每个厂商必须要有，而指向厂商的箭头是尖尖的箭头


# 联系上可能有属性(attribute on relationship)

![image-20201103170329104.png](https://i.loli.net/2020/11/11/uC84gqTfRi6K9ZA.png)

* 可以将联系的属性做成一个实体集

  ![image-20201103170437300.png](https://i.loli.net/2020/11/11/QzdowAFmRgPTNSq.png)

> 上图是多对多对一的联系，应该指出哪个是联系对应属性的实体
>
> 推荐使用上面不变成实体集的

# roles(tabels of one way relationships一元联系)

* 一元联系的标签

![image-20201103171437911.png](https://i.loli.net/2020/11/11/3A9jGDOPMB16zaU.png)

![image.png](https://i.loli.net/2020/11/14/SsnhIo2y7mCRDQl.png)

> 对称的联系

# 子类(sub classes)

![image-20201103171521797.png](https://i.loli.net/2020/11/11/u4ObFKoJaZRYLS6.png)

* 在面向对象过程中，一个对象只能属于一个类

* 但在E/R图中，一个对象可以属于好几个类，即如果实体e在一个子类中被描述，则在父类中也有相应的描述，并可以递归向上。也就是这两个表里面都有对e的描述的元组。

  ![image-20201103173139102.png](https://i.loli.net/2020/11/11/NbkOSD5hr1U4p3u.png)

# E/R图中的主键(keys)

* 在属性下面加下划线

  ![image-20201103173257755.png](https://i.loli.net/2020/11/11/lYkWxSViDm8AsqB.png)

  > 所有子类**继承**父类的**属性包括约束**

* multi-attributes key

  ![image-20201103173349216.png](https://i.loli.net/2020/11/11/sxM7YDIqnuAlciw.png)

  
# 度的约束(degree constaint)

* 一个酒吧最多销售10种啤酒

  ![image-20201103173528095.png](https://i.loli.net/2020/11/11/WeNzrZdjCu79xfp.png)

# 弱实体集(weak entity set)

* 要唯一识别E中的实体，要借助从E出发的联系的相关联的实体集的主键

  ![image-20201103174056411.png](https://i.loli.net/2020/11/11/wX6gZydfIjCBl1T.png)

> 队员中的name和number都不能作为主键，因为不同队伍的不同队员可能有相同名字和编号，所以要借助队伍这个实体集来帮助区分
>
> 这个联系称为支撑联系，且这个联系必须是多对一的，每个队员必须属于一个队伍，所以为圆圆箭头。
>
> 支撑联系可以有多个
>
> 弱实体集用双边框矩形来表示，联系也是双框
>
> 从弱实体集出发的联系不一定都是支撑联系
>
> 弱实体集的主键为：自身的属性和支撑联系对应的实体的主键联合形成主键

# 设计技巧

* 避免冗余

  saying the same thing in two different ways

  * 可能会造成数据不一致

    描述同一种东西的两个描述如果只改了一个不改另一个，会造成

    ![image-20201110163419938.png](https://i.loli.net/2020/11/11/R7Yh6tqLcXVr81x.png)

  * 浪费空间

* 避免使用弱实体集

* 能用属性就不用实体集

  * 实体集应该包含很多属性，除了key以外还有很多不是key的属性
  * 多对多联系和多对一联系中的“多”的一方，则用实体集
  
* 例子

  ![image.png](https://i.loli.net/2020/11/14/wptJchr8TNl1qsd.png)

  因为Beers时多对一联系中多的一方，所以用实体集。

  而manfs作为多对一联系中一的一方，而且只有一个name键属性，没有其它非主键属性，所以不适合做成一个实体集。

  应为：

  ![image.png](https://i.loli.net/2020/11/14/3o78B6MPCAH4jDn.png)

  再如下例：

  ![image.png](https://i.loli.net/2020/11/14/7rEJwsOXnzT1ZMB.png)

  这里beers的manf和manfs的addr存储的是相同的内容.出现了内容冗余

  正确的应为:

  ![image.png](https://i.loli.net/2020/11/14/3SOA785ZmCjFnMG.png)

  

# 从E/R图到数据库

* 实体集到关系

* 联系转换成关系，联系的属性为相关联的实体集的key
  * 多对多联系，联合主键
  * 多对一联系，多的实体集的key为主键，从而联系的关系和多的那个关系合并
  * 一对一联系，一个为主键，另一个unique约束
    * 可看成多对一的特殊情况，有时候可以将联系和关系合并，而有时候不能合并，看具体情况。
    * 一般来说联系所关联的两个实体集中那个属性少，那个和联系进行合并

* 处理若实体集

  * 支撑联系不用转换，除非有属性

* 子类转换(三种方法)

  * 面向对象的方式：每个子类都转换成一个关系，这个关系包含子类所有的属性(包括从父类继承来的)

  * use nulls：父类转换成关系，也包括所有子类的属性，有些元组不包含该属性则值为null

    可能空值会比较多

  * E/R style：子类全部转换成关系，只包括子类的key和特有的属性
  
  > 不同的转换方式，可能有的查询不利，有的查询有利，看具体情况

# 约束(constraint)

* 主键(实体完整性约束) primary-key

* 外键(参照完整性约束) foreign-key

* value-based constraints(用户自定义完整性约束)

* tuple-based constraint

* assertions

* 主键和唯一键不能重复，自动建立索引

# 外键，外键的值要参照另外一个关系中主键或唯一键的值

  * 与primary key 类似

  ```sql
  CREATE TABLE Beers (
  	name	  VARCHAR(20) PRIMARY KEY,
  	manf  VARCHAR(30) 
  );
  ```

  * after an attribute

  ```sql
  references <relation> (<attributes>)
  --example
  CREATE TABLE Sells (
  	bar    VARCHAR(20),
  	beer   VARCHAR(20) REFERENCES Beers(name),
  	price  REAL 
  );
  ```

  * 一系列

  ```sql
  foreign key(<list of attributes>)
  references <relation> (<attributes>)
  --example
  CREATE TABLE Sells (
  	bar		VARCHAR(20),
  	beer	VARCHAR(20),
  	price	REAL,
  	FOREIGN KEY(beer) REFERENCES Beers(name)
  );
  ```

* 外键的作用

  * If there is a foreign-key constraint from relation *R* to relation *S*, two violations are possible:

    * An insert or update to *R* introduces values not found in *S*.
  * conflict to the foreign key
    * A deletion or update to S causes some tuples of *R* to “dangle.”
      * conflict to the reference

* 设置参数

  * default

    若违反约束，则直接拒绝执行

  * cascade(集联)

    同步修改

  * set null

    设置为null

  ```sql
  CREATE TABLE Sells (
  	bar		VARCHAR(20),
  	beer	VARCHAR(20),
  	price	REAL,
  	FOREIGN KEY(beer) REFERENCES Beers(name)--后面的on是指对beers表进行删除或修改时的操作
  		ON DELETE SET NULL
  		ON UPDATE CASCADE
  );
  --没有on insert 因为对beersinsert不违反约束
  ```

  > 如果在beers中删除，则sells中啤酒为null
  >
  > 如果在beers中更新，则sells同步更新

# check约束

* 示例

  ```sql
  CREATE TABLE Sells (
  	bar		VARCHAR(20),
  	beer	VARCHAR(20),
  	price	REAL CHECK ( price <= 35.00 )
  );
  --check约束在insert或update时候进行判断
  ```

* 还有基于元组的check约束

  check约束还可以基于其它关系的属性(但是一些dbm没有实现该功能)

  ```sql
  CREATE TABLE Sells (
  		bar		VARCHAR(20),
  		beer		VARCHAR(20),
  		price	REAL,
  		CHECK (bar = 'HardRock' OR price <= 35.00)
  );
  ```

# modification of Constraints



# assertions(断言)

* 完成前面约束不能完成的功能

* 实例

  * 酒吧平均价格不能高于$5

  ```sql
  CREATE ASSERTION NoRipoffBars CHECK
  (
  	NOT EXISTS (
  		SELECT bar FROM Sells
  		GROUP BY bar
  		HAVING 5.00 < AVG(price)
  ));
  ```

  * 如果有操作会改变断言中的条件中的内容，则要进行判断，所以有时候比较耗时。

# triggers(触发器)

* 别名:event-condition-action rule (ECA Rule)
  * event

     typically a type of database modification, e.g., “insert on Sells.”

  * condition

    Any SQL boolean-valued expression.

  * action

    Any SQL statements.

* 实例

  Instead of using a foreign-key constraint and rejecting insertions into Sells(bar, beer, price) with unknown beers, a trigger can add that beer to Beers, with a NULL manufacturer.

  ```sql
  CREATE TRIGGER BeerTrig
  	AFTER INSERT ON Sells  --也可以为before在这个事件执行之前，执行触发器
  	REFERENCING
  		NEW ROW AS NewTuple
  	FOR EACH ROW
  	WHEN (NewTuple.beer NOT IN
  		(SELECT name FROM Beers))
  	   INSERT INTO Beers(name)
  		VALUES(NewTuple.beer);
  ```

  