# MYSQL的一些常用代码

## 列出所有数据库

```
mysql> SHOW DATABASE;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| shici              |
| sys                |
| test               |
| school             |
+--------------------+
```

其中，```information_schema```、```mysql```、```performance_schema```和```sys```是系统库，不要去改动它们。其他的是用户创建的数据库。

## 创建一个新数据库

假如想创建一个新数据库名字叫 newdatabase。

```
mysql> CREATE DATABASE newdatabase;
Query OK, 1 row affected (0.01 sec)
```

## 删除一个已有数据库

```
mysql> DROP DATABASE test;
Query OK, 0 rows affected (0.01 sec)
```

注意：删除一个数据库将导致该数据库的所有表全部被删除。

对一个数据库进行操作时，要首先将其切换为当前数据库：

```
mysql> USE newdatabase;
Database changed
```

> 表<br>
>
> 列出当前数据库的所有表，使用命令：
> ```
> mysql> SHOW TABLES;
> +---------------------+
> | Tables_in_test      |
> +---------------------+
> | classes             |
> | statistics          |
> | students            |
> | students_of_class1  |
> +---------------------+
> ```
>
> 要查看一个表的结构，使用命令：
> ```
> mysql> DESC students;
> +----------+--------------+------+-----+---------+----------------+
> | Field    | Type         | Null | Key | Default | Extra          |
> +----------+--------------+------+-----+---------+----------------+
> | id       | bigint(20)   | NO   | PRI | NULL    | auto_increment |
> | class_id | bigint(20)   | NO   |     | NULL    |                |
> | name     | varchar(100) | NO   |     | NULL    |                |
> | gender   | varchar(1)   | NO   |     | NULL    |                |
> | score    | int(11)      | NO   |     | NULL    |                |
> +----------+--------------+------+-----+---------+----------------+
> 5 rows in set (0.00 sec)
> ```



count();

| 函数 | 说明 |
|:-----|:-----|
|SUM|计算某一列的合计值，该列必须为数值类型|
|AVG|计算某一列的平均值，该列必须为数值类型|
|MAX|计算某一列的最大值|
|MIN|计算某一列的最小值|

**注意，MAX()和MIN()函数并不限于数值类型。如果是字符类型，MAX()和MIN()会返回排序最后和排序最前的字符。**

摘自[廖雪峰的官方网站](https://www.liaoxuefeng.com)
