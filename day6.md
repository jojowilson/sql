### 项目一
===
CREATE TABLE IF NOT EXISTS Trips (<br>
Id         INT, <br>
Client_Id  INT, <br>
Driver_Id  INT, <br>
City_Id    INT, <br>
Status     ENUM('completed', 'cancelled_by_driver', 'cancelled_by_client'), <br>
Request_at VARCHAR(50)<br>
);<br>

CREATE TABLE IF NOT EXISTS Users (<br>
Users_Id INT, <br>
Banned   VARCHAR(50), <br>
Role     ENUM('client', 'driver', 'partner')<br>
);<br>


TRUNCATE TABLE Trips;
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('1', '1', '10', '1', 'completed', '2013-10-01');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('2', '2', '11', '1', 'cancelled_by_driver', '2013-10-01');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('3', '3', '12', '6', 'completed', '2013-10-01');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('4', '4', '13', '6', 'cancelled_by_client', '2013-10-01');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('5', '1', '10', '1', 'completed', '2013-10-02');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('6', '2', '11', '6', 'completed', '2013-10-02');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('7', '3', '12', '6', 'completed', '2013-10-02');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('8', '2', '12', '12', 'completed', '2013-10-03');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('9', '3', '10', '12', 'completed', '2013-10-03');<br>
INSERT INTO Trips (Id, Client_Id, Driver_Id, City_Id, Status, Request_at) VALUES ('10', '4', '13', '12', 'cancelled_by_driver', '2013-10-03');<br>

TRUNCATE TABLE Users;<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('1',  'No',  'client');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('2',  'Yes', 'client');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('3',  'No',  'client');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('4',  'No',  'client');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('10', 'No',  'driver');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('11', 'No',  'driver');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('12', 'No',  'driver');<br>
INSERT INTO Users (Users_Id, Banned, Role) VALUES ('13', 'No',  'driver');<br>



select table2.Request_at,FORMAT(IFNULL(cancled_num/request_num,0),2) AS Cancellation_Rate<br>
from<br>
 
(SELECT n.Request_at,COUNT(n.Request_at) AS cancled_num<br>
  FROM<br>
 
			(SELECT t.Status,t.Request_at,u.Banned<br>
				FROM trips t<br>
					INNER JOIN users u<br>
			 WHERE (t.Request_at BETWEEN '2013-10-01' AND '2013-10-03')<br>
					AND (t.Client_Id = u.Users_Id )<br>
					AND u.Banned = 'No') AS n<br>
 WHERE n.Status !='completed'<br>
 GROUP BY n.Request_at) AS table1<br>
RIGHT JOIN<br>
(SELECT COUNT(n1.Request_at)AS request_num,Request_at<br>
FROM<br>
(SELECT t.Status,t.Request_at,u.Banned<br>
						FROM trips t<br>
							INNER JOIN users u<br>
					 WHERE (t.Request_at BETWEEN '2013-10-01' AND '2013-10-03')<br>
							AND (t.Client_Id = u.Users_Id )<br>
							AND u.Banned = 'No')AS n1<br>
GROUP BY Request_at)AS table2<br>
on table1.Request_at = table2.Request_at;<br>

### 项目二
===
INSERT INTO employee VALUES(1,'joe',70000,1),    <br>
				(2,'henry',80000,2),<br>
				(3,'sam',60000,2),<br>
				(4,'max',90000,1),<br>
			    (5,'janet',69000,1),<br>
			    (6,'randy',85000,1);<br>
				
				

# 查询语句
SELECT *<br>
FROM<br>
		((SELECT * <br>
		FROM<br>
		(SELECT d.Name AS department,e.Name AS Emoloyee,e.Salary<br>
			FROM employee e<br>
		 INNER JOIN department d<br>
		WHERE e.DepartmentId = d.Id<br>
		ORDER BY Salary DESC)AS n <br>
		WHERE department = 'IT'<br>
		LIMIT 3)<br>
  UNION<br>
		(SELECT *<br> 
				FROM<br>
				(SELECT d.Name AS department,e.Name AS Emoloyee,e.Salary<br>
					FROM employee e<br>
				 INNER JOIN department d<br>
				WHERE e.DepartmentId = d.Id<br>
				ORDER BY Salary DESC)AS n <br>
				WHERE department = 'Sales'<br>
				LIMIT 3))as table1;<br>
