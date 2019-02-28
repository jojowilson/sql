# 导入示例数据库
使用命令行导入： 教程 [MySQL导入示例数据库 -	MySQL教程™](https://www.yiibai.com/mysql/how-to-load-sample-database-into-mysql-database-server.html)
# 查询语句 SELECT FROM
SELECT是最常用的SQL语句，没有之一，它的用途是从一个或多个表中检索信息，使用SELECT检索信息，至少要给出两条信息：

- 想选择什么信息； 

- 从哪里选择信息； 
实例 
查询一列的数据 
```
SELECT contactLastName FROM customers --contactLastName是列标签，customers是表名
```
利用distinct语句去重
```
SELECT DISTINCT contactLastName FROM customers -- contactLastName是列标签，customers是表名
```
利用limit取前N个语句
```
SELECT  contactLastName FROM customers LIMIT 10 -- contactLastName是列标签，customers是表名

```
- 筛选语句 WHERE
WHERE 子句配合 SELECT 语句，表示有条件的筛选信息，类似程序语言中的if条件。  
where语句常结合运算符、通配符操作，运算符常见有算术运算符、逻辑运算符、比较运算符等。
- 算术运算符
“+”、“-”、“*”、“/”、“%”分别对应加减乘除求余。
- 比较运算符
“==”等于、“<=>”安全的等于、“<>(!=)”不等于、“<=”小于等于、“>=”大于等于、“IS NULL”判断一个值是否为NULL、“IS NOT NULL”判断一个值是否不为NULL。
逻辑运算符
NOT或者！ 逻辑非
AND或者&& 逻辑与
OR或者|| 逻辑或
XOR 逻辑异或
- 排序语句 ORDER BY
ORDER BY子句来设定你想按哪个字段哪种方式来进行排序，再返回搜索结果，常常配合ASC升序、DSEC降序使用。
实例
```
SELECT  country,count(*) as num  
	FROM customers 
	WHERE creditLimit > 0 
	GROUP BY country HAVING count(*) > 3
	ORDER BY country DESC ,count(*) ASC
 ```
 - 函数
 [MySQL函数](https://www.yiibai.com/mysql/functions.html)
 - SQL注释
“--”之后的文本属于注释。
```
SELECT NOW();-- 获得当前日期
```
“/**/”从/*开始，到*/结束，/*和*/之间的任何内容都是注释
# 作业1
```
-- 创建表
CREATE TABLE World (
name VARCHAR(50) NOT NULL,
continent VARCHAR(50) NOT NULL,
area INT NOT NULL,
population INT NOT NULL,
gdp INT NOT NULL
);


-- 插入数据
INSERT INTO World VALUES( 'Afghanistan', 'Asia',652230,25500100,20343000);
INSERT INTO World VALUES( 'Albania', 'Europe' ,28748,2831741,12960000);
INSERT INTO World VALUES( 'Algeria', 'Africa' ,2381741,37100000,188681000);
INSERT INTO World VALUES( 'Andorra' , 'Europe' ,468,78115,3712000);
INSERT INTO World VALUES( 'Angola' , 'Africa' ,1246700,20609294,100990000);
```
# 作业2
```
-- 创建表
CREATE TABLE email (
ID INT NOT NULL PRIMARY KEY,
Email VARCHAR(255)
)

-- 插入数据
INSERT INTO email VALUES('1','a@b.com');
INSERT INTO email VALUES('2','c@d.com');
INSERT INTO email VALUES('3','a@b.com');
```
