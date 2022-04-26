# 有关数据库的笔记
## 子查询与内连接哪个在sql server中性能更好或更快
### 我们什么时候应该使用内部加入？
### 我们什么时候应该使用子查询？
### 根据查询性能，哪一个将在SQL Server中更快？
#### 当我们需要使用多个表获取数据时，这些是常见的问题。这些问题没有直接的答案。在这里，我们将多方面讨论这一话题。
* 当我们需要在 SELECT 语句中从两个表中获取数据时，请使用连接。
* 当我们只需要从一个表中获取数据而另一个表仅用于检查是否存在时，请使用子查询。

例如：我们有两个表：tblEmp 和 tblEmpDetail 。
```
-- MySQL --
-- Emp --
CREATE TABLE Emp(
    EmpID BIGINT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
)

-- insert some recodes
INSERT INTO emp(EmpID, Name, Age) VALUES (10001, 'Name0001', 18);

-- EmpDetail --
CREATE TABLE EmpDetail(
    EmpDetailID BIGINT PRIMARY KEY,
    EmpID BIGINT REFERENCES tblEmp,
    Salary numeric,
    DOJ DATETIME
)

-- insert some recodes
INSERT INTO empdetail(EmpDetailID, EmpID, Salary, DOJ) VALUES(90001, 10001, 30000, '20220426');

```
内连接：通过使用内连接，我们可以选择两个表的字段。 例如：
```
SELECT
  E.EmpID,
  E.Name,
  E.AGE,
  ED.Salary,
  ED.DOJ
FROM Emp E INNER JOIN EmpDetail ED
  ON E.EmpID = ED.EmpID
```
子查询：我们可以从唯一的表中获取数据。 例如：
```
SELECT
  E.EmpID,
  E.Name,
  E.AGE
FROM Emp E
WHERE EmpID IN (SELECT EmpID FROM EmpDetail)
```
这里我们不能在查询字段中包含表 EmpDetail 的字段。因此，如果我们需要从两个表的字段中获取数据，join 是唯一的解决方案。子查询是不可能的。
当我们仅需要从一个表中获取数据，但是需要检查关联的另一个表中的是否存在相应数据时，可以通过连接和子查询来实现。在这种情况下，哪一个会执行更好呢？是内部连接还是子查询？  

在这里，我们以四种不同的方式编写了相同的查询：
不写了
