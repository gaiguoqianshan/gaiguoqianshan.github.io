---
layout: post
title: "SQlite基础语法"
date: 2016-03-10 09:03
comments: true
tags: 
	- Android
	- SQlite
---

### 1. 数据结构
* NULL　　：值是一个NULL值
* INTEGER ：值是一个带符号的整数
* REAL　　：值是一个浮点值
* TEXT　　：值是一个值是一个文本字符串
* BLOB　　：值是一个 blob 数据，完全根据它的输入存储
### 2. 创建表格
```
create table dataname.table_name(
_id integer primary autoincrement,
column2 datatype,
column3 datatype,
...
columnN datatype);
```
### 3. 删除表格
```
drop database_name.table_name;
```
### 4. 插入数据

```
insert into table_name(column1,column2,...columnN)]
values(value1,value2,...valueN);
/*为表中的所有列添加值，可省略列名*/
insert into table_name(value1,value2,...valueN);
```

### 5. 查询数据  

```java
select column1,column2,...columnN from table_name
/*查询所有列*/
select * from table_name
```
<!-- more -->

### 6. 逻辑运算符与where子句  

* AND : 允许在一个 SQL 语句的 WHERE子句中的多个条件的存在。
* BETWEEN ：用于在给定最小值和最大值范围内的一系列值中搜索值。
* EXISTS ：用于在满足一定条件的指定表中搜索行的存在。
* IN ：用于把某个值与一系列指定列表的值进行比较。
* NOT IN：用于把某个值与不在一系列指定列表的值进行比较。
* LIKE ：用于把某个值与使用通配符运算符的相似值进行比较。
* GLOB ：把某个值与使用通配符运算符的相似值进行比较。GLOB 与 LIKE 不同之处在于，它是大小写敏感的。
* OR ：用于结合一个 SQL 语句的 WHERE 子句中的多个条件。
* IS NULL ：用于把某个值与 NULL 值进行比较。
* IS 运算符与 = 相似。
* IS NOT 运算符与 != 相似。
* UNIQUE ：搜索指定表中的每一行，确保唯一性（无重复）。
* || ：连接两个不同的字符串，得到一个新的字符串。

假设 COMPANY 表有以下记录：
```
id   name     age    phone    salary
---  -----    ----   -----    ---------
1    Paul      32    127126   20000.0
2    Allen     25    116211   15000.0
3    Teddy     23    122711   20000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
6    Kim       22    127132   45000.0
7    James     24    121334   10000.0
```
下面的实例演示了 SQLite 逻辑运算符的用法。
`SELECT`语句列出AGE大于等于25且工资大于等于65000.00的所有记录：
```
select * from company where age >= 25 and salary >= 65000.00

id   name     age    phone    salary
---  -----    ----   -----    ---------
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
```
`SELECT`语句列出AGE大于等于25或工资大于等于65000.00 的所有记录：
```
select * from company where age >= 25 or salary >= 65000.00

id   name     age    phone    salary
---  -----    ----   -----    ---------
1    Paul      32    127126   20000.0
2    Allen     25    116211   15000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
```
`SELECT` 语句列出AGE不为 NULL 的所有记录 :
```
select * from company where age is not null
id   name     age    phone    salary
---  -----    ----   -----    ---------
1    Paul      32    127126   20000.0
2    Allen     25    116211   15000.0
3    Teddy     23    122711   20000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
6    Kim       22    127132   45000.0
7    James     24    121334   10000.0
```
`SELECT`语句列出NAME以'Ki'开始的所有记录，'Ki'之后的字符不做限制:
```
select * from company where name like 'ki%'

id   name     age    phone    salary
---  -----    ----   -----    ---------
6    Kim       22    127132   45000.0
```
`SELECT` 语句列出 AGE 的值为 25 或 27 的所有记录：
```
select * from company where age in (25,27)

id   name     age    phone    salary
---  -----    ----   -----    ---------
2    Allen     25    116211   15000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
```
`SELECT`语句列出 AGE 的值在 25 与 27 之间的所有记录：

```
select * from company where age between (25,27)

id   name     age    phone    salary
---  -----    ----   -----    ---------
2    Allen     25    116211   15000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
```

### 7. 修改数据

```
update table_name set 
column1=value1,column2=value2,...columnN=valueN 
where condition
```

### 8. 删除数据

```
delete from table_name where condition  
```

### 9. LIKE子句  

百分号（%）代表零个、一个或多个数字或字符。下划线（_）代表一个单一的数字或字符。这些符号可以被组合使用。
```
/*查找任意位置包含200的任意值*/
where salary like '%200%'
/*查找第二位为2，且以3结尾的任意值*/
where salary like '_2%3'
```

### 10. LIMIT子句

限制由 SELECT 语句返回的数据数量。
```
select * from company where limit 3 offset 2
/*从offset下一行开始*/
id   name     age    phone    salary
---  -----    ----   -----    ---------
3    Teddy     23    122711   20000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
```

### 11. ORDER BY 子句

基于一个或多个列按升序或降序顺序排列数据。
```
select column-list from table_name
where condition
order by column1,column2,...,columnN asc|desc
```

### 12. GROUP BY

“Group By”从字面意义上理解就是根据“By”指定的规则对数据进行分组，所谓的分组就是将一个“数据集”划分成若干个“小区域”，然后针对若干个“小区域”进行数据处理。
常见聚合函数:

>  | 函数           |     作用       |  
| --------       | :---------- :  | 
| sum(column)    |    求和      |  
| max(column)    |    最大值      |  
| min(column)    |    最小值      |  
| avg(column)　  |    平均值      |  
| count(column)  |  统计记录数    |

**例如：**我们在上面的company表格中插入几行得到新的company表格
　　
```
id   name     age    phone    salary
---  -----    ----   -----    ---------
1    Paul      32    127126   20000.0
2    Allen     25    116211   15000.0
3    Teddy     23    122711   20000.0
4    Mark      25    138228   65000.0
5    David     27    125352   85000.0
6    Kim       22    127132   45000.0
7    James     24    121334   10000.0
8    James     34    133234   25000.0
9    Paul      22    122126   20000.0
8    James     50    130034   35000.0
```
用`name column`对company进行分组,用having子句对group by限定条件
```
select name sum(salary) from company
group by name
having count(name) <= 2

name    salary
----    --------
Paul    40000.0
Allen   15000.0
Teddy   20000.0
Mark    65000.0
David   85000.0
Kim     45000.0
```
**注意：**
  
* 在聚合函数后不能再接select要选定的字段
* select语句的顺序
```
select
from
where
group by
having
order by
```

###13. Distinct关键字

DISTINCT关键字与SELECT语句一起使用，来消除所有重复的记录，并只获取唯一一次记录。
```
select distinct name from company
```
