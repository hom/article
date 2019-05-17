# MySql使用方式

## 数据库

### 连接数据库

```bash
mysql -uroot -p
# Enter password:
```

### 退出数据库

```bash
mysql>exit
# Bye
```

### 创建数据库

> CREATE DATABASE database_name

#### 在命令行中创建

```bash
create database PONGJ;
```

#### 使用`mysqladmin`创建

```bash
mysqladmin -u root -p create PONGJ
# Enter password:
```

### 删除数据库

> DROP DATABASE database_name

#### 命令行中删除

```bash
drop database pongj;
```

#### 使用`mysqladmin`删除

```bash
mysqladmin -u root -p drop pongj
# Enter password:
```

### 切换数据库

```bash
mysql>user pongj;
```

## 数据表

### 创建数据表

> CREATE TABLE table_name (column_name column_type);

```bash
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

### 删除数据表

> DROP TABLE table_name;

```bash
mysql>drop table table_name;
```

### 插入数据

```bash
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```

### 查询数据

#### 基本语句

```bash
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]
```

#### WHERE语句

```bash
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
```

#### UPDATE语句

```bash
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE Clause]
```

#### DELETE语句

```bash
DELETE FROM table_name [WHERE Clause]
```

#### LIKE语句

```bash
SELECT field1, field2,...fieldN 
FROM table_name
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue'
```

#### UNION语句

```bash
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT]
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

#### 排序语句

```bash
SELECT field1, field2,...fieldN table_name1, table_name2...
ORDER BY field1, [field2...] [ASC [DESC]]
```

#### 分组

```bash
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name;
```
