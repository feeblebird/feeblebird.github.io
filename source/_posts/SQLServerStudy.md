---
title: SQLServerStudy
date: 2020-10-12 19:47:16
tags:Transact SQL(sql在microsoft sql server上的加强版本)
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

# SQLServer添加一行

```sql
alter table tablename newcolumn type;
```

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
```





