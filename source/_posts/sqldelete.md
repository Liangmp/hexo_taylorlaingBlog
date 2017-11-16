---
title: 数据库删除语句drop,delete和truncate的区别
date: 2017-11-16 15:26:59
tags:
  - SQL
categories:
  - SQL
---
drop,delete和truncate都是删除命令，但是用起来有很大差别，drop用于删除表，delete用于删除表中的某一行或多行，truncate用于清空表格中的数据。<!--more-->

## Drop
drop用于删除表
语法：
```sql
Drop  Table 表名称
```

## Delete
delete用于删除表中的某一行或多行
语法：
'''sql
-- 删除某一行
Delete From 表名称  Where 列名称=值
-- 删除某一行
Delete From 表名称  Where 列名称=值
-- 或     
Delete *  From  表名称
'''

## Truncate
truncate用于清空表格中的数据，保留表格的结构、属性和索引等。
语法：
```sql
truncate Table 表格名称
```

truncate的用法有点类似于
```sql
-- 复制tableA的表格结构到tableB，但是不复制tableA里面的数据
select * into tableB from tableA where 1 = 0; 
```