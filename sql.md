## 创建数据库

```sql
 CREATE DATABASE employee
```

## 创建数据表

CREATE TABLE 表名(
<span style="vertical-align:super;"> 字段名 字段属性, </span>
<span style="vertical-align:super;"> 字段名 字段属性, </span>
<span style="vertical-align:super;">)</span>

```sql
CREATE TABLE employee(id INT PRIMARY KEY,name varchar(100),age INT,department_id INT)
```

## 字段的增删改查

### 增加

ALTER TABLE 表名 ADD 列名 属性

```sql
ALTER TABLE employee ADD tel varchar(11)
```

### 删除

 ALTER TABLE 表名  DROP column 列名

```sql
ALTER TABLE employee DROP column test</span>
```

### 修改

#### 修改字段属性

- **mysql**

​    ALTER TABLE 表名 MODIFY 列名 属性

```mysql
ALTER TABLE mmmsql MODIFY name varchar(80)
```

- **sql**

​    ALTER TABLE 表名 ALTER COLUMN 列名 属性

```sql
  ALTER TABLE employee alter COLUMN name varchar(80)
```

#### 修改字段名

- mysql
  
  ALTER TABLE 表名 RENAME COLUMN 列名 to 新列名

```mysql
 1.ALTER TABLE mmmsql RENAME COLUMN name to xm VARCHAR(20) NOT NULL
 2.ALTER TABLE   mmmsql  CHANGE COLUMN name xm VARCHAR(20) NOT NULL
```

## 索引

索引是一种数据结构，用于加快数据库查询的速度和性能，**类似于书的目录**

​    索引：普通索引和唯一索引

​    区别是唯一索引确保索引中的值是唯一的，不允许有重复值

### 创建索引

- 普通索引

```mysql
CREATE INDEX 索引名 ON 表明(字段名)
CREATE index ererer on ryxx(name)
```

### 修改索引

#### 添加索引

可以使用 **ALTER TABLE** 命令可以在已有的表中创建索引。

ALTER TABLE 允许你修改表的结构，包括添加、修改或删除索引。

ALTER TABLE 创建索引的语法：

```sql
ALTER TABLE table_name ADD INDEX index_name (column1 [ASC|DESC], column2 [ASC|DESC], ...)
```

- `ALTER TABLE`: 用于修改表结构的关键字。
- `table_name`: 指定要修改的表的名称。
- `ADD INDEX`: 添加索引的子句。`ADD INDEX` 用于创建普通索引。
- `index_name`: 指定要创建的索引的名称。索引名称在表中必须是唯一的。
- `(column1, column2, ...)`: 指定要索引的表列名。你可以指定一个或多个列作为索引的组合。这些列的数据类型通常是数值、文本或日期。
- `ASC` 和 `DESC`（可选）: 用于指定索引的排序顺序。默认情况下，索引以升序（ASC）排序。

```sql
ALTER TABLE 表名 add INDEX 索引名 (字段1,字段2)
ALTER TABLE ryxx add INDEX inddd (sex,name)
```

#### 删除索引

```mysql
1.ALTER TABLE 索引名 drop INDEX 索引名
ALTER TABLE ryxx drop INDEX inddd2
2.DROP INDEX 索引名 ON 表名
DROP INDEX inddd ON ryxx
```

## 视图

​    SQL 中的视图是一个虚拟表，是 基于 sql 查询的结果创建的，视图本身不存储数据，是对数据库实际表的查询结果的一个抽象。视图是动态的，一旦表中的数据发生改变，显示在视图中的数据也会发生改变。同样对视图的更新，会影响到原来表的数据

​    作用: 用于存储数据表的查询结果

​    特点: 安全，可自定义显示列，具有唯一性

### 创建视图

```sql
CREATE VIEW 视图名 AS
SELECT
字段1, 字段2, ...
FROM 表名
WHERE 条件
#创建年龄大于17的视图表CREATE CREATE VIEW AGE_OVER_17 AS 
CREATE VIEW AGE_OVER_17 AS 
SELECT
    name,
    age
FROM
    students 
WHERE
    age > 17
```

视图结果

![image-20240617092559675](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240617092559675.png)

### 更新视图

​    由于视图是数据表的查询结果，是一个动态的表，在数据表更新之后视图表也会跟着改变

```sql
UPDATE students
SET age = 333
WHERE id = 1
```

数据更新后的视图

![image-20240617093104237](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240617093104237.png)

### 删除视图

```sql
DROP VIEW AGE_OVER_17
DROP VIEW IF EXISTS AGE_OVER_17 ##IF EXISTS是检测视图是否存在，如果存在即删除
```

## 主键

主键是用来标识每一行数据的字段，具有唯一性和非空性

就像身份证号，每个人都只有唯一一个，人名可以重复但身份证号不重复

### 创建主键

在创建数据表的时候可以创建主键

```MYSQL
CREATE TABLE employee (
    id int PRIMARY key,
    name VARCHAR(20) not  null
)
```

也可以实用命令创建

```sql
 1.MYSQL
 ALTER TABLE 表名 ADD PRIMARY key(主键字段) 
 ALTER TABLE employee ADD PRIMARY key(id) 
 2.SQL
   2.1ALTER TABLE 表名 ADD PRIMARY key(主键字段) 
   2.2ALTER TABLE 表名 ADD CONSTRAINT 主键名 PRIMARY KEY(主键字段)
```

### 删除主键

```SQL
1.MYSQL
ALTER TABLE 表名 DROP PRIMARY KEY
2.SQL
ALTER TABLE 表名 DROP CONSTRAINT 主键名
```

## 字段数据增删改查

### 增加数据

​    INSERT INTO 语句用于向表中插入新记录

```SQL
#INSERT INTO 表名 (字段1,字段2,字段3) VALUES (数据1,数据2,数据3)
INSERT INTO `employe`.`employee` (`id`, `name`, `sex`, `age`, `department_id`, `tel`) VALUES (4, '刁筝望', 1, 22, 1004, '18036043129')#添加数据
####在不指定字段名时，需要把每一项数据按顺序写上
INSERT INTO `employe`.`employee` VALUES (4, '刁筝望', 1, 22, 1004, '18036043129')
```

### 删除数据

​    DELETE 用于删除表中数据

```sql
DELETE FROM 表名 WHERE 条件
DELETE  FROM employee WHERE id = 11
```

### 修改数据

​    UPDATE 用于修改表中的数据

​    **执行 UPDATE 数据一定要带上条件**   在 MySQL 中可以通过设置 **sql_safe_updates** 这个自带的参数来解决，当该参数开启的情况下，你必须在 update 语句后携带 where 条件，否则就会报错。**set sql_safe_updates = 1;** 表示开启该参数

```sql
UPDATE 表名 SET 新数据1,新数据2,..... WHERE 条件1,条件2,....
UPDATE employee SET age='11' where id = 1
```

### 查询数据

#### 一般查询

​	SELECT * FROM   *可以是单个字段或多个字段，如果不写咋显示所有数据

```sql
SELECT * FROM 表名 WHERE 条件
SELECT * FROM employee WHERE id =1 #显示所有id为1的数据
SELECT name FROM employee WHERE id =1 #只显示id为1的name列数据
```

#### 去重查询

​    SELECT DISTINCT 用于返回唯一不同的值，就是不显示重复的值

```sql
SELECT DISTINCT department FROM employee 
```

#### 条件查询

| 符号              | 含义   | 语法                                                                               |
| --------------- | ---- |:--------------------------------------------------------------------------------:|
| >               | 大于   | SELECT * FROM employee WHERE age > 30                                            |
| <               | 小于   | SELECT * FROM employee WHERE age < 30                                            |
| =               | 等于   | SELECT * FROM employee WHERE age = 30                                            |
| != 或 <>           | 不等于  | SELECT * FROM employee WHERE age != 30                                           |
|''或 null         | 空    | SELECT * FROM employee WHERE age = ''  SELECT * FROM employee WHERE age is  null |
|BETWEEN  .. AND | 区间   | SELECT * FROM employee WHERE age BETWEEN 30 AND 50  #年龄 30-50 之间                   |
| AND 或&&          | 和，且  | SELECT * FROM employee WHERE age < 50 AND SEX = 1  #年龄小于 50 且性别为女性                 |
| OR 或\|\|         | 或    | SELECT * FROM employee WHERE age < 50 OR department_id = 1                       |
| LIKE(%)、LIKE(_) | 模糊查询 | SELECT * FROM employee  WHERE name LIKE '张_' #查询名字包含张的 2 个字的名字  所有包含使用 LIKE '张%'    |
| in(...)         | 多条件  | SELECT * FROM employee WHERE age in(40,60,80) #查询年龄是 40 60 80 的数据                  |

[^LIKE(%)、LIKE(_)]: LIKE(_)表示查询有一个字符的数据   LIKE(%X)表示查询带有 X 的数据  前面无论有多少位，只要结尾是 X 的数据

#### 聚合查询

| 符号    | 含义  | 语法                                                   |
|:-----:|:---:|:----------------------------------------------------:|
| COUNT | 计数  | SELECT COUNT(sex) AS '女' FROM employee WHERE sex = 0 |
| MAX   | 最大值 | SELECT MAX(age) FROM employee                        |
| MIN   | 最小值 | SELECT MIN(age) FROM employee                        |
| AVG   | 平均值 | SELECT AVG(age) FROM employee                        |
| SUM   | 求和  | SELECT SUM(age) FROM employee                        |

#### 分组查询

- `GROUP BY` 语句中的列必须出现在 `SELECT` 语句中。
- `SELECT` 语句中的列要么是分组列，要么是聚合函数的结果。

| 符号       | 含义     | 描述                     | 语法                                                      |
|:--------:|:------:| ---------------------- |:-------------------------------------------------------:|
| GROUP BY | 分组查询   | 根据一个或多个列对结果集进行分组。      | SELECT SEX, COUNT(*) FROM employee GROUP BY SEX          |
| HAVING   | 分组结果筛选 | 把分组查询侯的结果进行筛选，类似于 WHERE | SELECT 分组列, 聚合函数 FROM employee 条件 GROUP BY 分组列 HAVING 条件 |

```sql
#实用group by分组并且附加条件查询时，需要把条件写在 group by前面
SELECT   department_id,COUNT(*) FROM employee  WHERE age <45 AND department_id >5  GROUP BY department_id 
```

```sql
#HAVING会把分组侯的结果再进行筛选，下面例子是  以部门ID为分组统计年龄小于45的且部门人数大于80的人数
SELECT   department_id,COUNT(*) FROM employee  WHERE age <45    GROUP BY department_id  HAVING  COUNT(*) >80
```

#### 排序查询

​    排序查询分为 DESC 和 ASC    DESC 为降序  ASC 为升序

```sql
SELECT * FROM employee  ORDER BY 字段 排序方式1,字段 排序方式2
#通过年龄降序，收入正序查询
SELECT * FROM employee  ORDER BY age DESC,shouru ASC
```

#### 分页查询

- MYSQL

   分页查询  LIMIT  N  表示查询前 N 条数据，LIMIT N, M  表示查询从 N 条开始共 M 条数据

| 符号            | 含义                       | 语法                                     |
| --------------- | -------------------------- | ---------------------------------------- |
| LIMT N          | 返回前 N 条数据              | SELECT * FROM employee LIMIT  3          |
| LIMT N, M        | 返回从 N+1 条开始的前 M 条数据 | SELECT * FROM employee LIMIT  3,10       |
| LIMT N OFFSET M | 返回从 M+1 开始的前 N 条数据   | SELECT * FROM employee LIMIT  10 OFFSET3 |

 LIMIT N, M 和 LIMT N OFFSET M 得到的结果相同

```mysql
SELECT * FROM 表名    LTMIT 起始索引，查询记录数     索引从0开始
SELECT * FROM employee LIMIT  3,10 #表示从第三条数据开始，一共显示10条
SELECT * FROM employee LIMIT  3  #显示前三条数据
```

- ------

  SQL

  1. SQL 分页查询必须要用 ORDER BY 排序，不排序也要设置一个虚拟字段
  2. SQL 分页查询要实用 OFFSET 和 FETCH NEXT

  OFFSET ...FETCH NETX  跳过...获取下一个

```sql
SELECT * FROM 表名 ORDER BY 字段名 OFFSET 偏移量(跳过前多少条) ROWS FETCH NEXT 查询量(显示多少条) ROWS ONLY
SELECT * FROM employee ORDER BY 1 OFFSET 10 ROWS#跳过前10条数据，从第11条数据开始
SELECT * FROM employee ORDER BY 1 OFFSET 10 ROWS FETCH NEXT 10 ROWS ONLY#跳过前10条数据，从第11条数据开始显示10条

```

## 多表查询

​	SQL中JOIN用于把来自两个或多个表的行结合起来。

![img](https://www.runoob.com/wp-content/uploads/2019/01/sql-join.png)

| 符号          | 含义                                     | 语法                                                         |
| ------------- | ---------------------------------------- | ------------------------------------------------------------ |
| INNER JOIN ON | 如果表中有至少一个匹配，则返回行         | SELECT * FROM employee  INNER JOIN department ON department.id = employee.department_id |
| LEFT  JOIN ON | 即使右表中没有匹配，也从左表返回所有的行 | SELECT * FROM employee LEFT JOIN department  ON department.id = employee.department_id |
| RIGHT JOIN ON | 即使左表中没有匹配，也从右表返回所有的行 | SELECT * FROM employee RIGHT JOIN department  ON department.id = employee.department_id |
|               |                                          |                                                              |

### INNER JOIN ON

​	INNER JOIN 关键字在表中存在至少一个匹配时返回行。

