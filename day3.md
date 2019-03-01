# MySQL表数据类型
MySQL支持所有标准SQL数值数据类型。
这些类型包括严格数值数据类型(INTEGER、SMALLINT、DECIMAL和NUMERIC)，以及近似数值数据类型(FLOAT、REAL和DOUBLE PRECISION)。
关键字INT是INTEGER的同义词，关键字DEC是DECIMAL的同义词。
BIT数据类型保存位字段值，并且支持MyISAM、MEMORY、InnoDB和BDB表。
作为SQL标准的扩展，MySQL也支持整数类型TINYINT、MEDIUMINT和BIGINT。下面的表显示了需要的每个整数类型的存储和范围。 
# 用SQL语句创建表
创建MySQL数据表需要以下信息：
- 表名
- 表字段名
- 定义每个表字段
```
CREATE TABLE table_name (column_name column_type);
```
以下例子中我们将在 RUNOOB 数据库中创建数据表runoob_tbl：
```
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
   `runoob_id` INT UNSIGNED AUTO_INCREMENT,
   `runoob_title` VARCHAR(100) NOT NULL,
   `runoob_author` VARCHAR(40) NOT NULL,
   `submission_date` DATE,
   PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
实例解析：
- 如果你不想字段为 NULL 可以设置字段的属性为 NOT NULL， 在操作数据库时如果输入该字段的数据为NULL ，就会报错。
- AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。
- PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔。
- ENGINE 设置存储引擎，CHARSET 设置编码。
# 用SQL语句向表中添加数据
MySQL 表中使用 INSERT INTO SQL语句来插入数据。 
语法
以下为向MySQL数据表插入数据通用的 INSERT INTO SQL语法：
 ```
INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );
```
如果数据是字符型，必须使用单引号或者双引号，如："value"。
# 用SQL语句删除表
MySQL中删除数据表是非常容易操作的， 但是你再进行删除表操作时要非常小心，因为执行删除命令后所有数据都会消失。 
语法
以下为删除MySQL数据表的通用语法：
```
DROP TABLE table_name ;
```
在命令提示窗口中删除数据表
在mysql>命令提示窗口中删除数据表SQL语句为 DROP TABLE ：
实例
以下实例删除了数据表runoob_tbl:
```
root@host# mysql -u root -p
Enter password:*******
mysql> use RUNOOB;
Database changed
mysql> DROP TABLE runoob_tbl
Query OK, 0 rows affected (0.8 sec)
mysql>
```
删除表内数据，用 delete。格式为：
```
delete from 表名 where 删除条件;
```
实例：删除学生表内姓名为张三的记录。
```
delete from  student where  T_name = "张三";
```
清除表内数据，保存表结构，用 truncate。格式为：
```
truncate table 表名;
```
实例：清除学生表内的所有数据。
```
truncate  table  student;
```
删除表用 drop，就是啥都没了。格式为：
```
drop  table  表名;
```
实例：删除学生表。
```
drop table student;
```
1、当你不再需要该表时， 用 drop; 
2、当你仍要保留该表，但要删除所有记录时， 用 truncate;
3、当你要删除部分记录时， 用 delete。
# 用SQL语句修改表
当我们需要修改数据表名或者修改数据表字段时，就需要使用到MySQL ALTER命令。
删除、修改或添加字段
首先创建一张表，表明testalter_tbl:
```
create table testalter_tbl
    (
    i INT,
    c CHAR(1)
    );
 ```
 # 作业

### 项目三：超过5名学生的课（难度：简单）

创建如下所示的courses 表 ，有: student (学生) 和 class (课程)。

**注：插入数据字符串数据已经要加‘’， 字段不需要**

创建表格

```mysql
CREATE TABLE courses(
	student VARCHAR(100) NOT NULL,
    class VARCHAR(100) NOT NULL,
)
```

插入数据

```mysql
INSERT INTO courses 
(student, class)
VALUES
('A', 'Math'),
('B', 'English'),
('C', 'Math'),
('D', 'Biology'),
('E', 'Math'),
('F', 'Computer'),
('G', 'Math'),
('H', 'Math'),
('I', 'Math'),
('A', 'Math');
```

例如,表:

| student | class      |
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
| A       | Math       |

编写一个 SQL 查询，列出所有超过或等于5名学生的课。

应该输出:

| class   |
|----|
| Math    |

Note:
学生在每个课中不应被重复计算。

查询数据：

```mysql
SELECT class FROM courses GROUP BY class HAVING COUNT(*) > 5;
```

**注：写语句时刻记得FROM table**

### 项目四：交换工资（难度：简单）


创建表格

```mysql
CREATE TABLE salary (
	id INT UNSIGNED AUTO_INCREMENT, 
	name VARCHAR(100) NOT NULL,
	sex VARCHAR(100) NOT NULL,
	salary INT UNSIGNED NOT NULL,
	PRIMARY KEY (id)
);
```

插入数据

```MYSQL
INSERT INTO salary 
(name, sex, salary)
VALUES
('A', 'm', 2500),
('B', 'f', 1500),
('C', 'm', 5500),
('D', 'f', 500);
```

**注：直接update会有顺序无法实现**

```mysql
UPDATE salary SET sex = 'f' WHERE sex = 'm';
UPDATE salary SET sex = 'm' WHERE sex = 'f';
```

所以使用CASE WHEN 进行更新

当满足某一条件时，执行某一result

```mysql
case  
    when condition then result
    when condition then result
    when condition then result
else result
end
```

```mysql
UPDATE salary
	SET sex = 
CASE WHEN sex = 'f'
	THEN sex = 'm'
	ELSE sex = 'f'
	END;
```

利用replace交换函数：

```mysql
UPDATE salary
SET sex = REPLACE('m',sex,'f')
```
