---
title: SQLServerStudy
date: 2020-10-12 19:47:16
tags:
	-Transact SQL(sql在microsoft sql server上的加强版本)
	-SQL
categories: SQL
---

# T-SQL简介

* **SQL Server** 用于操作数据库的编程语言为**Transaction-SQL** ，简称 **T-SQL**

* SQL和T-SQL的区别

  **SQL** 作为结构化查询语言，是标准的关系型数据库通用的标准语言；**T-SQL**是在 **SQL** 基础上扩展了延伸的函数、系统预存程序以及**程序设计** 结构的 **SQL Server** 中使用的语言

# SQLServer中修改列表属性的语句

```sql
alter table tablename alter column columnname newtype;
--修改数据类型的时候要保障改属性不是主键，否则要先删除主键
```

> SQLServer中没有Modify关键字，用alter column关键字

# SQLServer中修改列表属性从空设置为不空，或反之

```sql
--相当于重新设置数据类型，只是数据类型相同，后面跟了not null或null
alter table tablename alter column columnname newtype not null;
```

# SQLServer中删除主键

```sql
alter table tablename drop constraint 主键名称;
--主键名称在表中查看，或者执行sp_help tablename;命令查询。
```

>注意SQL Server中的主键名字中是**两个下划线连着的**。

# SQLServer添加一列

```sql
alter table tablename add newcolumn type;
--注意不能加column
```

> 不管原表中是否有该列的数据，新加后统一位NULL

# SQL check约束

```sql
--在创建表的过程中添加约束
creat table tablename
(
   	num int,
    check(num>0)
);
```

* 若已经创建了num属性，而是要添加约束则

```sql
alter table tablename
add check(num>0);

alter table tablename
add unique();

alter table tablename
add constraint name unique();--设置约束名字

alter table tablename
add primary key();

alter table tablename
add constraint name primary key();--设置主键名字
```

# SQL 设置约束名称

```sql
create table test
(
	num int constraint PK_num primary key 
);
```

# SQL Server中的索引

还没学

# transact-SQL插入数据

```sql
insert into tablename(attribute1,attribute2,attribute3,attribute4)
values(data1,data2,data3,data4);

insert into tablename
values(data1,data2,data3,...);
--插入的是表中的全部数据时才能直接用这个。
```

# SQL外键

> 外键用于与另一张表的关联。是能确定另一张表记录的字段，数据库强制你保持数据的一致性。

* 外键的作用

  我们先建有外键关联的两张表

![image.png](https://i.loli.net/2020/10/21/pghWeO9jMt4P5UJ.png)

​		然后在course表中插入一条数据

```sql
INSERT INTO tb_course (StuId, CourseName, Score) VALUES (1, 'java基础', 80);
```

​		然后报错了

![image.png](https://i.loli.net/2020/10/21/KeWmHut1M4BhnCr.png)

​		原因就是Student表中并没有主键Id为1的这条记录，那么就不能在Course表中插入这叫记录。

​		接下来我们在Student表中插入一条记录，并且主键的Id为1

![image.png](https://i.loli.net/2020/10/21/cv2EfGosqQM8yu7.png)

​		然后我们接着执行这条sql语句

```sql
INSERT INTO tb_course (StuId, CourseName, Score) VALUES (1, 'java基础', 80);
```

​		就可以执行成功

* 同样地，修改删除操作也是如此，不能破坏表中的关系，简单地说，就是不能给Student表中不存在的学生成绩。
  而且删除的时候得先删除外键表再删除主键表
  例如：如果我把Student表中数据删除了，那么Course表中StuId = 1的这个学生就不存在了，所以数据库不会让你删。

* 外键的设置

  ```sql
  CREATE TABLE Orders
  (
  Id_O int NOT NULL,
  OrderNo int NOT NULL,
  Id_P int,
  PRIMARY KEY (Id_O),
  FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)
  )
  ```

  ```sql
  ALTER TABLE Orders
  ADD FOREIGN KEY (Id_P)
  REFERENCES Persons(Id_P)
  ```


# select attribute1

```sql
select all attribute1         --默认是select all
select distinct attribute1    --去重复是select distinct
```

 # SQL 中确定数据范围

```sql
select attribute1
from table
where attribute1 between 20 and 23; 
--在20-23中的

select attribute1
from table
where attribute1 not between 20 and 23;
--不在20到23中的
```

# 查询中属性一升序，属性二降序

```sql
select *
from table
order by attribute1 ASC,attribute DESC;
```

# group by 和 group by all

* 只有在有where语句时，这个才有意义
* group by 只显示符合where条件的分组
* group by all显示全部的分组，不符合where条件的分组，对应的属性值为null

# group by 后面多个字段

* group by后面多个字段的意思就是，这几个字段联合起来进行分组

* 但是分组是有先后顺序的

  ```sql
  group by attribute1,attribute2;
  ```

  > 分组的顺序是先attribute2，再attribute1
  >
  > 即先按照attribute2进行分组，分好之后再在分组中按照attribute1进行分组


# datetime录入时要加引号

# 查询问题

* **查询选修了全部课程的学生姓名**

  * 方法一：集合的交、并、差

    ```sql
    select sname
    from student s1
    where not exists
    (
    	(
        	select cno
            from course
        )
        except
        (
        	select cno
            from student_course
            where sno = s1.sno
        )
    );
    ```

  * 方法二：谓词的转换(双重否定等于肯定)

    > 选修了全部课程
    >
    > ==>
    >
    > 不存在课程他没选

    ```sql
    select s1.sname
    from student s1
    where not exists
    (
    	select cno
        from course c1
        where not exists
        (
        	select cno
            where sno = s1.sno and cno = c1.cno
        )
    );
    ```

* 至少选修了学生201215122选修的全部课程的学生号码

  * 方法一：集合的交、并、差

    ```sql
    select s1.sno
    from student s1
    where not exists
    (
    	(
        	select cno
            from student_course
            where sno = s1.sno 
        )
        union
        (
        	select cno
            from stduent_course
            where sno = '201215122'
        )
        except
        (
            select cno
            from 
        )
    ) and sno <> '201215122';
    ```

  * 方法二：谓词的转换(双重否定等于肯定)

    > 至少选修了学生201215122选修的全部课程
    >
    > ==>
    >
    > 不存在201215122选修的课程该学生没选

    ```sql
    select s1.sno
    from student s1
    where not exists
    (
    	select cno
        from 
        (
        	select cno
            from student_course
            where sno = '201215122'
        )new
        where not exists
        (
        	select cno
            from student_course sc1
            where sc1.sno = s1.sno and sc1.cno = new.cno
        )
    ) and sno <> '201215122';
    ```

# 集合的除运算

![image.png](https://i.loli.net/2020/11/02/1X8kEVZcdGLNPuI.png)

> 包含(b1,c2),(b2,c1),(b2,c3)的集合R中的只有a1，则R÷S的结果就为a1

# 视图的修改

* 视图或表的重命名

  ```sql
  alter table tbname
  rename to newtbname; --改表名
  --这是sql中的语句，sql server中没有rename关键字
  EXEC sp_rename '原表名','新表名';
  ```

* 视图或表的属性重命名

  ```sql
  alter table tbname
  change column bir birthday datetime; --修改属性名，类型必须要加，可以认为这里的修改就是删除原来的属性而添加一个新的属性，约束也可以改变。  
  --上面是sql中的修改列名
  --sql server中为
  修改列名：EXEC sp_rename ‘表名.[原有列名]’, ‘新列名' , 'COLUMN';
  EXEC sp_rename 'ASYR_Dispatch.[OrderId]', 'Order_Id' , 'COLUMN
  ```


# SQL SERVER中的视图

* 虚拟视图

  ```sql
  create view viewname[(attribute1,attribute2...)]
  as 
  	select attribute1,attribute2...
  	from tablename
  	where condition;
  ```

  > 可以指定及给子查询结果列的重命名，不指定则根据结果列名进行填充

* 物化视图(索引视图)

  ```sql
  create view V_Computer[(attribute1,attribute2...)]
  with schemabinding
  as
  	select attribute1,attribute2...
  	from tablename
  	where condition;
  ```

* 两者区别

  > 虚拟视图进行查询和修改的时候DBM会将我们的语句转换成对基本表的语句。
  >
  > 因为虚拟视图不是设计存储在数据库中
  >
  > 而
  >
  > 物化视图则是实际存储在数据库中的一个视图，所以查询时不用进行语句转换
  >
  > 但是更改的时候还是要在基本表中进行插入，删除等等

# SQL SERVER中的索引

```sql
CREATE [ UNIQUE ] [ CLUSTERED | NONCLUSTERED ] INDEX index_name   
    ON <object> ( column_name [ ASC | DESC ] [ ,...n ] )   
    [ WITH <backward_compatible_index_option> [ ,...n ] ]  
    [ ON { filegroup_name | "default" } ]  
--unique参数：为表或视图创建唯一索引。唯一索引不允许两行具有相同的索引键值。视图索引必须唯一。如果要建唯一索引的列有重复值，必须先删除重复值。
--clustered参数：表示指定创建的索引为聚集索引。创建索引时，键值的逻辑顺序决定表中对应行的物理顺序。聚集索引的底层(或称叶级别)包含该表的实际数据行。
--nonclustered：表示指定创建的索引为非聚集索引。创建一个指定表的逻辑排序的索引。对于非聚集索引，数据行的物理排序独立于索引排序。
--[ ASC | DESC]参数：表示指定特定索引列的升序或降序排序方向。 默认值为 ASC。
<object> ::=  
{  
    [ database_name. [ owner_name ] . | owner_name. ]   
    table_or_view_name  
}  
  
<backward_compatible_index_option> ::=  
{   
    PAD_INDEX  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB  
  | IGNORE_DUP_KEY  
  | STATISTICS_NORECOMPUTE   
  | DROP_EXISTING   
}
```

* 创建索引

  ```sql
  create index ind_sname on student(sname DESC);
  create unique index ind_cname on course(cname);
  --因为创建表时，创建主键自动创建聚集索引，所以在其它列上创建聚集索引，要先把主键删除掉
  alter table student_course
  drop constraint PK__student___63D81FA334066AB2;
  --只要是更改表，都要指出是哪个表
  --表的属性的修改都是
  --alter table tablename
  --表的列的值修改都是
  --update tablename
  --这个删除表的索引
  --drop index indexname on tablename;
  --删除表，删除视图，则知名数据库就可,use dbname
  create clustered index ind_sno on student_course(sno);
  alter table student_course
  add constraint PK_snotcid primary key(sno,tcid);
  create index ind_snotcidscore on student_course(sno ASC,tcid ASC,score DESC);
  drop index ind_sno on student_course;
  ```
```
  

# SQL SERVER中的架构

* 类似于C++中的namespace
* 如果不指定登录用户的话，默认的是dbo即database owner
* 我们创建的表、视图等等都会在架构中，所以如果一些语句不指定架构，则dbm不知到该去找哪个表。



# T-SQL常量

* 字符串常量

  ```sql
  'sql','数据库'
```

* 时间值常量

  ```sql
  '2020-11-09'
  ```

* 货币常量

  ```sql
  $124.5
  ```

* 数值型常量

  ```sql
  123,1.2,3
  ```

# T-SQL变量

* 局部变量

  ```sql
  @var
  ```

* 全局变量

  ```sql
  @@var
  ```

* T-SQL内置全局变量

  * @@ERROR

    **返回最后执行的**Transact-SQL语句的错误代码。没有错误则为零

  * @@ROWCOUNT

    返回受上一语句影响的行数，任何不返回行的语句将这一变量设置为0

  * @@SERVERNAME

    返回本地服务器的名称

  * @@VERSION

    返回SQL Server当前安装的日期、版本和处理器类型

* 打印输出变量

  ```sql
  print @@VERSION;
  select @@SERVERNAME;
  ```

* 变量的声明

  变量在使用前必须先声明才能使用

  * 声明局部变量的语法

    ```sql
    declare @varname datatype;
    --例如
    declare @A INT;
    ```

* 变量的赋值

  * 局部变量有两种方式赋值

    * set

      ```sql
      set @varname = value
      --例如
      set @A = 3
      ```

    * select

      ```sql
      select @varname1 = value1,@varname2 = value2
      --例如
      set @A = attribute1,@B = attribute2
      from tablename;
      ```

    * 区别

      set只能给一个变量进行赋值，select可以给多个变量赋值

# if-else语句

* 语法格式

  ```sql
  if(condition)
  	begin
  		...
  	end
  else
  	begin
  		...
  	end
  ```

  > **begin…end**相当于**c**语言中的大括号，有多条语句才使用**begin…end**，相当于**begin…end**之间的语句就是一个语句块
  
  ```sql
  --判断是否是闰年
  declare @year int;
  set @year=1900;
  if(@year%4 = 0 and @year%100 <>0 or @year%400 = 0)
  	begin
  		 print(cast(@year as varchar)+'是闰年');
  	end
  else
  	begin
  		print(cast(@year as varchar)+'不是闰年');
  	end
  ```

# case-end多分支语句

* 语法格式

  ```sql
  case
  	when 条件1 then 结果1
  	when 条件2 then 结果2
  	else 其它结果
  end
  ```

  例如

  ```sql
  select stuNo,成绩= case
           when writtenExam<60 then 'E'
           when writtenExam between 60 and 69 then 'D'
           when writtenExam between 70 and 79 then 'C'
           when writtenExam between 80 and 89 then 'B'
           else  'A'
  end    --或者end 成绩 如下：
  from stuMarks;
  select stuNo,case
           when writtenExam<60 then 'E'
           when writtenExam between 60 and 69 then 'D'
           when writtenExam between 70 and 79 then 'C'
           when writtenExam between 80 and 89 then 'B'
           else  'A'
  end '成绩'
  from stuMarks;
  ```
  
  ```sql
  select name,publisher,author,
  	case
  		when cost>50 then '定价太高，不适合作教材'
  		else '定价'+cast(cost as varchar(10))+'，可以作教材'
  	end '是否可以作为教材'
  from books b1;
  --或者
  select name,publisher,author,'是否可以作为教材'= case
  		when cost>50 then '定价太高，不适合作教材'
  		else '定价'+cast(cost as varchar(10))+'，可以作教材'
  	end 
  from books b1;
  ```
  
  > 相当于使用case定义了一列属性

# 循环结构while

* 语法格式

  ```sql
  while(conditon)
  	begin
  		语句或语句块
  	end
  ```

* continue,break,return关键字

  * continue
  * break
  * return

* 例如

  ```sql
  declare @sum int,@i int;
  select @i=1,@sum=0;
  while @i <= 100
  begin
  	select @sum = @sum + @i;
  	select @i = @i + 1;
  end
  print '1...100的和为：'+convert(char(4),@sum);
  
  declare @jie int,@i2 int;
  select @jie=1,@i2=1;
  while @i2 <= 10
  begin
  	select @jie = @jie*@i2;
  	select @i2 = @i2+1;
  end
  print '10的阶乘为：'+convert(char(10),@jie);
  
  --筛选素数
  declare @i3 int,@i4 int,@flag int;
  select @i3 = 2,@i4 = 2,@flag=0;
  while @i3 <= 100
  begin
  	select @i4 = 2;
  	while(@i4<@i3)
  	begin
  		select @flag=0;
  		if(@i3%@i4=0)
  		begin
  			select @flag=1;
  			break;
  		end
  		select @i4 = @i4 + 1;
  	end
  	if(@flag=0)
  	begin
  		print @i3;
  	end
  	select @i3 = @i3 + 1;
  end
  ```

# T-SQL类型转换函数

* cast函数

  ```sql
  cast(expression as date_type[(length)])
  select cast(@price1 as int)
  select cast(定价 as varchar(5))
  ```

* convert函数

  ```sql
  convert(data_type[(length)],expresion[,style])
  select convert(int,@price1)
  print convert(char(4),@SUM)
  select convert(varchar(100),getdate(),1);
  ```

* > 输出变量+字符串时，要先把变量转换为字符串

# T-SQL日期函数

* 返回相应字段的整数值

  * 方式1

  ```sql
  day(date_expression)
  month(date_expression)
  year(date_expression)
  --返回日期常量中的相应字段的整数值
  ```

  * 方式2

  ```sql
  datepart(<datepart>,<date>)
  datepart(dd,date)--等同于day(date)
  datepart(mm,date)--等同于month(date)
  datepart(yy,date)--等同于year(date)
  ```

  > 注意方式一和方式二的返回值都为整数值

* 返回相应字符的字符串形式

  ```sql
  datename(<datepart>,<date>)
  --形式和datepart一样
  ```

* 返回当前的日期和时间

  ```sql
  getdate()
  ```

* 通过加减日期和时间间隔来计算并显示日期和时间

  ```sql
  dateadd(datepart,number,datecolumnname)
  --datepart计算的单位，为day,month,year还是其它
  --number相应值
  --datecolumnname就是基准时间
  --例如
  select dateadd(day,10,getdate());
  --返回当前日期时间后10天的日期和时间
  ```

* 返回两个指定时间之间的间隔，返回值为一个带正负号的整数

  ```sql
  datediff(datepart,startdate,enddate);
  --例如
  select datediff(year,'2015',getdate());
  ```

# T-SQL存储过程(Stored Procedure)

*  存储过程是一组为了完成特定功能的SQL语句集，经编译后存储在数据库中。
* 用户通过指定存储过程的名字并给出参数(如果该存储过程带有参数)来执行它。
* 

