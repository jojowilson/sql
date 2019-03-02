<center><font size=5 color='green'>MySQL别名</font></center>

```sql
SELECT cust_name, cust_contact
FROM Customers AS C, Orders AS O, OrderItems AS OI
WHERE C.cust_id = O.cust_id
AND OI.order_num = O.order
```
<p>　　FROM子句中的三个表全都有别名。在WHERE子句中就可以用别名代替表名了。</p>
1. INNER JOIN

```sql
SELECT vend_name, prod_name, prod_price
FROM Vendors INNER JOIN Products
ON Vendors.vend_id = Products.vend_id;
```
<p>　　此语句中的SELECT与前面的SELECT语句相同，但FROM子句不同。这里，两个表之间的关系是以INNERJOIN指定的部分FROM子句。在使用这种语法时，联结条件用特定的 ON子句而不是 WHERE子句给出。传递给ON的实际条件与传递给WHERE的相同。</p>
2.自联结

```sql
SELECT c1.cust_id, c1.cust_name, c1.cust_contact
FROM Customers AS c1, Customers AS c2
WHERE c1.cust_name = c2.cust_name
AND c2.cust_contact = 'Jim Jones';
```
<p>　　此查询中需要的两个表实际上是相同的表，因此Customers表在 FROM子句中出现了两次。虽然这是完全合法的，但对Customers的引用具有歧义性，因为 DBMS不知道你引用的是哪个Customers表。</p>
<p>　　解决此问题，需要使用表别名。Customers第一次出现用了别名 C1，第二次出现用了别名C2。现在可以将这些别名用作表名。例如，SELECT语句使用C1前缀明确给出所需列的全名。如果不这样，DBMS将返回错误，因为名为 cust_id、cust_name、cust_contact的列各有两个。DBMS不知道想要的是哪一列（即使它们其实是同一列）。WHERE首先联结两个表，然后按第二个表中的cust_contact过滤数据，返回所需的数据。</p>
3.LEFT JOIN
要检索包括没有订单顾客在内的所有客户

```sql
SELECT Customers.cust_id, Orders.order_num
FROM Customers LEFT OUTER JOIN Orders
ON Customers.cust_id = Orders.cust_id;
```
<p>　　类似上一课提到的内联结，这条SELECT语句使用了关键字OUTERJOIN来指定联结类型（而不是在 WHERE子句中指定）。但是，与内联结关联两个表中的行不同的是，外联结还包括没有关联行的行。在使用 OUTERJOIN语法时，必须使用 RIGHT或 LEFT关键字指定包括其所有行的表（RIGHT指出的是OUTERJOIN右边的表，而LEFT指出的是OUTERJOIN左边的表）。上面的例子使用 LEFT OUTER JOIN从 FROM子句左边的表（Customers表）中选择所有行。为了从右边的表中选择所有行，需要使用RIGHT OUTER JOIN</p>
4.UNION

```sql
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN ('IL','IN','MI')
UNION
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_name = 'Fun4All';
```
<p>　　这条语句由前面的两条SELECT语句组成，之间用UNION关键字分隔。UNION指示 DBMS执行这两条SELECT语句，并把输出组合成一个查询结果集。UNIONM默认会删除所有重复的行，可以使用UNION ALL。</p>
5.CROSS JOIN

```sql
SELECT * FROM [TABLE 1] CROSS JOIN [TABLE 2]

或者：SELECT * FROM [TABLE 1], [TABLE 2]
```
<p>　　笛卡尔积</p>
<font size=6>项目一</font>

```sql
SELECT person.FirstName,person.LastName,address.City,address.State FROM person LEFT OUTER JOIN address ON person.PersonId=address.PersonId
```
<font size=6>项目二</font>

```sql
SELECT id,Email from email WHERE ID in (SELECT MIN(ID) FROM email GROUP BY Email)
```
