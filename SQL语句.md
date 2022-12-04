# SQL语句注意事项

• SQL **commands** are case insensitive: • Same: SELECT, Select, select
 • Same: Student, student
 • Same: gpa, GPA

sql命令语句中 大小写无所谓

• **Values** are **not:
** • Different: 'SFU', 'sfu'

但是在value里面 区分大小写

• SQL strings are enclosed in **single quotes**

​	• e.g. name = 'Mike’

​	• Single quotes in a string can be specified using an initial single quote character as an escape

​		• author='ShaqO''Neal'
 • Strings can be compared **alphabetically** with the comparison operators
​	 • e.g. 'fodder' < 'foo' is TRUE (String里面可以对String字符串进行比较)



## 创建table

```sqlite
CREATE TABLE Customer (
sin CHAR(20) primary key,
firstName CHAR(11),
lastName CHAR(20),
age INTEGER
)
```



## Insert语句

### 插入数据

``` sqlite
INSERT INTO Customer(sin, firstName, lastName, age)
VALUES ('111', 'Sam', 'Spade', 23)

```

插入了一行数据

### 插入列

```sqlite
ALTER TABLE Customer ADD height INTEGER
```

插入了一个列





## Delete语句

```sqlite
DELETE

FROM Customer 

WHERE sin = '111'
```



## Update语句

```sqlite
UPDATE Customer 

SET age = 37 

WHERE sin = '111'
```





## Drop语句

### drop table

```sqlite
DROP TABLE Customer
```





## Select语句

### Ordered语法

```sqlite
SELECT name,gpa,age
FROM	students
WHERE school = 'SFU'
ORDER BY gpa DESC, age ASC
```



### LIKE 语法

```sqlite
SELECT * 
FROM students
WHERE name LIKE 'Sm_t%'
```

- The **%** symbol stands for zero or more arbitrary characters

  %后面可以是任意数量字符

- The **_** symbol stands for exactly one arbitrary character

  “_"符号代表一个占位符 可以是任意

- The **%** and **_** characters can be escaped with **\****

  

- **  • E.g., name **LIKE** ’Michael\_Jordan'

  ​	 

### DISTINC 语法

```sqlite
SELECT DISTINCT School #对于school这一列
FROM   Students
```





## NULL 相关

```sqlite
CREATE TABLE Students (
  name CHAR(20) NOT NULL,
  age CHAR(20) NOT NULL,
	gpa FLOAT
)
```

Two Important Rules

1、Arithmetic operations (+, -, *, /) on nulls return **NULL**

2、Comparisons with nulls evaluate to **UNKNOWN

​	NULL = NULL will return Unknown

**Truth Value** table for result:

+ true  **OR** unknown = true

+ False **OR** unknown = unknown
+ unknown **OR** *unknown* = unknown
+ true **AND** unknown = unknown
+ false **AND** unknown  = false
+ unknown **AND** unknown = unknown

1. The result of a **WHERE** clause is treated as *false* if itevaluates to unknown

+ WHERE unknown  --->  false



## 多表查询

**Multiple tables** （数据存多表）

1. Data updating is easier (e.g., update Mary’s gpa to 3.9)

2. Querying each individual table is faster (e.g., retrieve Mary’s gpa)

 **A single table** （数据存单表）
	 1. Data exchange is easier (e.g., share your data with

others)

2. Avoid the cost of joining multiple tables (e.g., retrieval all the courses that Mary has taken)

### 1. Foreign Key constraints

 Foreign-key constraint:
 • **student_id** references **sid**

```sqlite
 CREATE TABLE Enrolled(
      student_id CHAR(20),
      cid        CHAR(20),
      grade      CHAR(10),
      PRIMARY KEY (student_id, cid),
			FOREIGN KEY (student_id) REFERENCES Students(sid) 
)
```



#### 错误示例：

![image-20220204151132557](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204151132557.png)

注意： students里面的sid 必须和 Enrolled里面的student_id保持一致；

注意：sid必须作为Students的主键

不能多 不能少



#### 正确示例：

![image-20220204151157107](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204151157107.png)

#### Insert operations:

如果在Enrolled table里面insert了新的student_id 并且不与Students里面的sid匹配

**INSERT REJECT**



#### Delete operations:

1. 如果我们准备删除Students里面的sid 在Enrolled table 有对应的student_id时 应该删除失败 所以应该：Disallow the delete *(ON DELETE RESTRICT)*

**restrict(约束)**:当在父表（即外键的来源表）中删除对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除。

##### ON DELETE RESTRICT

```sqlite
CREATE TABLE Enrolled(
  student_id CHAR(20),
  cid CHAR(20),
  grade CHAR(10),
  PRIMARY KEY (student_id, cid),
  FOREIGN KEY (student_id) REFERENCES Students(sid) ON DELETE RESTRICT
)
```

2. 如果我们想要删除一个学生 who enroll了course
   + 删除这个学生enroll的all courses  *(ON DELETE CASCADE)*

**cascade(级联):**当在父表（即外键的来源表）中删除对应记录时，首先检查该记录是否有对应外键，如果有则也删除外键在子表（即包含外键的表）中的记录。

##### ON DELETE CASCADE

```sqlite
 CREATE TABLE Enrolled(
  student_id CHAR(20),
  cid CHAR(20),
  grade CHAR(10),
  PRIMARY KEY (student_id, cid),
  FOREIGN KEY (student_id) REFERENCES Students(sid) ON DELETE CASCADE
)
```

3. 如果我们想删除一个学生 who enroll了course
   +  Set Foreign Key to NULL (ON DELETE SET NULL)

**set null:**当在父表（即外键的来源表）中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null（不过这就要求该外键允许取null）

```sqlite
CREATE TABLE Enrolled(
  student_id CHAR(20),
  cid CHAR(20),
  grade CHAR(10),
  PRIMARY KEY (student_id, cid),
  FOREIGN KEY (student_id) REFERENCES Students(sid) ON DELETE SET NULL
)
```

### 2. Joins （basic）

Example: 

![image-20220204154828263](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204154828263.png)

![image-20220204154841441](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204154841441.png)

#### Join’s sql

```sqlite
//三种方法写join
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND
       cid = 354 AND grad = ‘A+’
 
SELECT name
FROM   Students
JOIN   Enrolled ON sid = student_id
WHERE cid = 354 AND grad = ‘A+’
 
SELECT name
FROM   Students
JOIN   Enrolled ON sid = student_id
       AND cid = 354 AND grad = ‘A+’
```

#### 多表列重名

![image-20220204155428939](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204155428939.png)

每个表中 都有 name col

```sqlite
//两种方法
SELECT Students.name
FROM Students, Enrolled 
WHERE sid = student_id

//
SELECT S.name
FROM Students S, Enrolled 
WHERE sid = student_id
```

#### ①. INNER JOIN

它将合并结果集中两个表中的行数据。

![image-20220205193744442](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205193744442.png)

```sqlite
SELECT name, course
FROM Student 
INNER JOIN Enroll 
ON name = stdName
```



#### ②. FULL  JOIN

FULL JOIN 即為LEFT JOIN 與RIGHT JOIN 的聯集，它會返回左右資料表中所有的紀錄，不論是否符合連接條件。

```sqlite
SELECT name, course
FROM Student FULL JOIN Enroll 
ON name = stdName
```

![image-20220205200557631](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205200557631.png)

#### ③. LEFT JOIN

```sqlite
SELECT name
FROM Student LEFT  JOIN Enroll 
ON name = stdName
```

![image-20220205200505559](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205200505559.png)

#### ④. RIGHT JOIN

```sqlite
SELECT name
FROM Student RIGHT JOIN Enroll 
ON name = stdName
```

![image-20220205200536270](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205200536270.png)



### 3. Joins: SQL semantics

![image-20220204172554280](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220204172554280.png)



### 4. Set Operations

#### UNION(并集)

![image-20220205005155441](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205005155441.png)

SQLite的 **UNION** 子句/运算符用于合并两个或多个 SELECT 语句的结果，不返回任何重复的行。

为了使用 UNION，每个 SELECT 被选择的**列数必须是相同**，相同数目的列表达式，相同的数据类型，并确保它们有相同的顺序，但它们不必具有相同的长度。

![image-20220205004116111](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205004116111.png)

UNION方法

```sqlite
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 354
UNION
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 454
```

普通方法:

```sqlite
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND (cid = 354 OR cid = 454)
```



⚠️⚠️⚠️ 上面是找到 either 354 or 454

⚠️⚠️⚠️下面是找到 Both 354 and 454

#### INTERSECT(相交)

![image-20220205004916706](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205004916706.png)

![image-20220205004255820](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205004255820.png)

普通方法：

```sqlite
SELECT name
FROM Students S, Enrolled E1, Enrolled E2
WHERE S.sid = E1.student_id AND S.sid = E2.student_id
       AND (E1.cid = 354 AND E2.cid = 454)
```

INTERSECT方法：

```sqlite
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 354
INTERSECT
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 454
```

#### EXCEPT(除去)

![image-20220205005129398](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205005129398.png)

![image-20220205005101221](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205005101221.png)

EXCEPT方法：

```sqlite
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 354
EXCEPT
SELECT name
FROM   Students, Enrolled
WHERE  sid = student_id AND cid = 454
```

#### Duplicates(重复)

Sqlite的UINION INTERSECT EXCEPT默认是不重复的

但是我们可以通过**ALL**来取消默认不重复

示例：

```sqlite
SELECT name
FROM Students, Enrolled
WHERE sid = student_id AND cid = 354 
INTERSECT ALL
SELECT name
FROM Students, Enrolled
WHERE sid = student_id AND cid = 454
```



## **Aggregation**

![image-20220205201111201](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205201111201.png)

**agg** = COUNT, SUM, AVG, MAX, MIN, etc.

* Except count, all aggregations apply to a single attribute

![image-20220205201154029](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205201154029.png)

![image-20220205201225343](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205201225343.png)



## Group and Agg

```sqlite
SELECT agg(column)
FROM   <table name>
WHERE  <conditions>
GROUP BY <columns>
```

• How to get AVG(gpa) for each gender?

```sqlite
SELECT AVG(gpa) 
FROM Student 
GROUP BY gender
```

![image-20220205202006655](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205202006655.png)

注意⚠️：

### Invalid Section

Select后面只能包括 groupby的 或者 agg( )的

![image-20220205202306930](/Users/zhangchenkun/Library/Application Support/typora-user-images/image-20220205202306930.png)



## Having Clause

Having语句必须和Group by一起用

类似于多一个条件语句 where

不同的是：

WHERE 子句在所选列上设置条件，而 HAVING 子句则在由 GROUP BY 子句创建的分组上设置条件。

```sqlite
SELECT agg(column)
FROM   <table name>
WHERE  <conditions>
GROUP BY <columns>
HAVING <columns>
```





## Subqueries

```sqlite
-- Outer Query
SELECT C.customerID, C.birthDate, C.income 
FROM Customer C
WHERE C.customerID IN
-- Outer Query

-- Inner Query
(
SELECT O.customerID
FROM Account A, Owns A
WHERE A.accNumber = O.accNumber
AND A.branchName = 'Lonsdale’
)
-- Inner Query
```

### intermediate table 中间表

**Rule of thumb: avoid nested queries when possible**

```sqlite
SELECT firstName, lastName, MAX(sumBalance)
FROM 
(
	SELECT firstName, lastName, sum(balance) AS sumBalance
	FROM Customer C, Account A, Owns O 
	WHERE C.customerID = O.customerID
	AND O.accNumber = A.accNumber 
  GROUP BY C.customerID 
)AS T
WHERE T.sumBalance = 0
```



### Subqueries constant

Subqueries return a single constant  >,<,=,<>,>=,<=

```sqlite
SELECT C1.customerID
FROM Customer C1
WHERE C1.income > (SELECT avg(C2.income)
										FROM Customer C2)
```



### Subqueries relation

+ IN 
+ NOT IN 
+ EXISTS
+ NOT EXISTS
+ ANY 
+ ALL

1. Find the customerIDs of customers with an account at the Burnaby branch

```sqlite
SELECT C.customerID
FROM Customer C
WHERE C.customerID IN (SELECT O.customerID
												FROM Account A, Owns O
												WHERE A.accNumber = O.accNumber 
                       		AND A.branchName = ’Burnaby’
                       )
```

2. Find the customerIDs of customers who do *not* have an account at the Burnaby branch

   ```sqlite
   SELECT C.customerID
   FROM Customer C
   WHERE C.customerID NOT IN (
     													SELECT O.customerID
   														FROM Account A, Owns O
   														WHERE A.accNumber = O.accNumber																AND A.branchName = ’Burnaby’)
   ```

   

3. Find the customerIDs of customers with an account at the Burnaby branch

   ```sqlite
   SELECT C.customerID 
   FROM Customer C 
   WHERE EXISTS ( SELECT *
   								FROM Account A, Owns O
   								WHERE C.customerID = O.customerID
   									AND A.accNumber = O.accNumber 
                 		AND A.branchName = ’Burnaby’)
   ```

   EXISTS and NOT EXISTS test whether the associated sub-query is non-empty or empty

4. **Have an account in all branches**

   ```sqlite
   SELECT C.customerID
   FROM Customer C
   WHERE NOT EXISTS ( (SELECT B.branchName
   										FROM Branch B) 
                     EXCEPT
   								(SELECT A.branchName
   									FROM Account A, Owns O
   									WHERE O.customerID = C.customerID
   									AND O.accNumber = A.accNumber)
                    )
   ```

5. Find the customerIDs of customers who earn more than *some* customer called Bruce

   ⚠️：

   Customers in the result table must have incomes greater than at least one of the rows in the sub-query result

   ```sqlite
   SELECT C.customerID 
   FROM Customer C 
   WHERE C.income > ANY
   							(SELECT Bruce.income
   								FROM Customer Bruce
   								WHERE Bruce.firstName = 'Bruce')
   ```

   

6. Find the customerIDs of customers who earn more than *all* customer called Bruce

   ```sqlite
   SELECT C.customerID 
   FROM Customer C 
   WHERE C.income > ALL
                     (SELECT Bruce.income
                     FROM Customer Bruce
                     WHERE Bruce.firstName = 'Bruce')
   ```

   If there were **no** customers **called Bruce** this query would return **all customers**