---
title: SQLServerStudy
date: 2020-10-12 19:47:16
tags:
	-Transact SQL(sql在microsoft sql server上的加强版本)
	-SQL
categories: SQL
---

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

>注意SQL Server中的主键名字中是两个下划线连着的。

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
add constraint primary key();--设置主键名字
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