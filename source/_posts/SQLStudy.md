---
title: SQLStudy
date: 2020-09-19 19:09:02
tags: SQL
categories: SQL
---

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

* #### 转义字符

  ```sql
  'i''m liwei' => i'm liwei
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

# 转义字符 \

# NULL

* 与其他进行运算值都是NULL

* 与其他值比较结果为unknow

* 判断是否为空

  where is now; / where is not null;


# 多表查询，多关系查询

```sql
SELECT l1.drinker
FROM likes l1,likes l2,likes l3
WHERE l1.drinker = l2.drinker AND l1.drinker = l3.drinker
AND l1.beer < l2.beer AND l2.beer < l3.beer;SELECT l1.drinker
FROM likes l1,likes l2,likes l3
WHERE l1.drinker = l2.drinker AND l1.drinker = l3.drinker
AND l1.beer < l2.beer AND l2.beer < l3.beer;
```

