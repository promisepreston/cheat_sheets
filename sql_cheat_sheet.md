# SQL Cheat Sheet

## Glossary
**SQL**: SQL is a standard language for accessing and manipulating databases. It stands for Structured Query Language.
**RDBMS**: RDBMS stands for Relational Database Management System. It is the basis for SQL, and for all modern database systems such as MS SQL Server, IBM DB2, Oracle, MySQL, and Microsoft Access.
**Table**: A table is a collection of related data entries and it consists of columns and rows. The data in RDBMS is stored in database objects called tables.
**Semicolon**: A semicolon is the standard way to separate each SQL statement in database systems that allow more than one SQL statement to be executed in the same call to the server.
**SQL Stored Procedures for SQL Server**: A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again. So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it. You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

    **Stored Procedure Syntax**
    CREATE PROCEDURE procedure_name
    AS
    sql_statement
    GO;

    **Execute a Stored Procedure**
    EXEC procedure_name;


    **Stored Procedure Example**
    The following SQL statement creates a stored procedure named "SelectAllCustomers" that selects all records from the "Customers" table:

    CREATE PROCEDURE SelectAllCustomers
    AS
    SELECT * FROM Customers
    GO;

    **Execute the Stored Procedure**
    EXEC SelectAllCustomers;


    **Stored Procedure With One Parameter**
    The following SQL statement creates a stored procedure that selects Customers from a particular City from the "Customers" table:

    CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
    AS
    SELECT * FROM Customers WHERE City = @City
    GO;

    **Execute the Stored Procedure**
    EXEC SelectAllCustomers @City = 'London';


    **Stored Procedure With Multiple Parameters**
    The following SQL statement creates a stored procedure that selects Customers from a particular City with a particular PostalCode from the "Customers" table:

    CREATE PROCEDURE SelectAllCustomers @City nvarchar(30), @PostalCode nvarchar(10)
    AS
    SELECT * FROM Customers WHERE City = @City AND PostalCode = @PostalCode
    GO;

    **Execute the Stored Procedure**
    EXEC SelectAllCustomers @City = 'London', @PostalCode = 'WA1 1DP';

**SQL Comments**: Comments are used to explain sections of SQL statements, or to prevent execution of SQL statements.

    **Single Line Comments(--)**
    --Select all:
    SELECT * FROM Customers;

    SELECT * FROM Customers -- WHERE City='Berlin';


    **Multi-line Comments (start with /* and end with */)**
    /*SELECT * FROM Customers;
    SELECT * FROM Products;
    SELECT * FROM Orders;
    SELECT * FROM Categories;*/
    SELECT * FROM Suppliers;    

## Data Control Language (DCL) Commands
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
GRANT | Used to assign permission to users to access database objects.
REVOKE | Used to deny permission to users to access database objects.

## Data Definition Language (DDL) Commands
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
ALTER | Adds, deletes, or modifies columns in a table, or changes the data type of a column in a table.
BACKUP DATABASE | Creates a back up of an existing database. | **For MS SQL Server**<br>BACKUP DATABASE databasename<br>TO DISK = 'filepath'; | **For MS SQL Server**<br>BACKUP DATABASE testDB<br>TO DISK = 'D:\backups\testDB.bak';
CREATE | Creates a database, index, view, table, or procedure.<br><br>**Note**: Make sure you have admin privilege before creating any database. Once a database is created, you can check it in the list of databases with the following SQL command: `SHOW DATABASES`; | CREATE DATABASE databasename; | CREATE DATABASE testDB;
CREATE TABLE | Creates a new table in the database. | **Create a Single Table**<br>CREATE TABLE table_name (<br>__column1 datatype,<br>__column2 datatype, ....<br>);<br><br>**Create a Table From Another Table**<br>CREATE TABLE new_table_name AS<br>__SELECT column1, column2,...<br>__FROM existing_table_name<br>__WHERE ....; | **Create a Single Table**<br>CREATE TABLE Persons (<br>__PersonID int,<br>__LastName varchar(255),<br>__FirstName varchar(255),<br>);<br><br>**Create a Table From Another Table**<br>CREATE TABLE TestTable AS<br>SELECT customername,<br>contactname<br>FROM customers;
DROP | Deletes a column, constraint, database, index, table, or view.<br><br>**Note**: Be careful before dropping a database. Deleting a database will result in loss of complete information stored in the database! | DROP DATABASE databasename; | DROP DATABASE testDB;

## Data Manipulation Language (DML) Commands
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
DELETE | Delete rows from a table | DELETE FROM table_name<br>WHERE condition; | **DELETE Single Record**<br>DELETE FROM Customers<br>WHERE CustomerName='Alfreds Futterkiste';<br><br>**DELETE All Records**<br>DELETE FROM Customers;
INSERT INTO | Inserts new rows in a table.<br><br>**Note**: You do not insert values into a primary key like `id`, `CustomerID`, since it is an **auto-incremented** field | INSERT INTO table_name (column1, column2, ...)<br>VALUES (value1, value2, value3, ...); | INSERT INTO Customers (CustomerName, City, Country)<br>VALUES ('Cardinal', 'Stavanger', 'Norway');
INSERT INTO SELECT | Copies data from one table into another table | **Copy all columns from one table to another table**<br>INSERT INTO table2<br>SELECT * FROM table1<br>WHERE condition;<br><br>**Copy only some columns from one table into another table**<br>INSERT INTO table2 (column1, column2, ...)<br>SELECT column1, column2, ...<br>FROM table1<br>WHERE condition; | **Copy all columns from one table to another table**<br>INSERT INTO Customers (CustomerName, City, Country)<br>SELECT SupplierName, City, Country FROM Suppliers;<br><br>**Copy only some columns from one table into another table**<br>INSERT INTO Customers (CustomerName, City, Country)<br>SELECT SupplierName, City, Country FROM Suppliers<br>WHERE Country='Germany';
UPDATE | Updates existing rows in a table<br><br>**Note**: Be careful when updating records. If you omit the WHERE clause, ALL records will be updated! | UPDATE table_name<br>SET column1 = value1, column2 = value2, ...<br>WHERE condition; | **UPDATE Single Record**<br>UPDATE Customers<br>SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'<br>WHERE CustomerID = 1;<br><br>**UPDATE Multiple Records**<br>UPDATE Customers<br>SET ContactName='Juan'<br>WHERE Country='Mexico';

## Data Query Language (DQL) Commands
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
SELECT | Select data from a database | **Select all columns**<br>SELECT * FROM table_name;<br><br>**Select some columns**<br>SELECT column1, column2, ...<br>FROM table_name; | **Select all columns**<br>SELECT * FROM Customers;<br><br>**Select some columns**<br>SELECT CustomerName, City FROM Customers;
SELECT DISTINCT | Selects only distinct (different) values | SELECT DISTINCT column1, column2, ...<br>FROM table_name;<br><br>SELECT COUNT(DISTINCT column)<br>FROM table_name; | SELECT DISTINCT Country FROM Customers;<br><br>SELECT COUNT(DISTINCT Country) FROM Customers;
SELECT INTO | Copy all columns into a new table | **Copies data from one table into a new table**<br>SELECT * <br>INTO newtable [IN externaldb]<br>FROM oldtable<br>WHERE condition;<br><br>**Copy only some columns into a new table**<br>SELECT column1, column2, ...<br>INTO newtable [IN externaldb]<br>FROM oldtable<br>WHERE condition; | **Copy all columns into a new table**<br>SELECT * INTO CustomersBackup2017<br>FROM Customers;<br><br>SELECT * INTO CustomersBackup2017<br>FROM Customers<br>WHERE Country = 'Germany';<br><br>**Copy only some columns into a new table**<br>SELECT CustomerName, ContactName INTO CustomersBackup2017<br>FROM Customers;<br><br>SELECT Customers.CustomerName, Orders.OrderID<br>INTO CustomersOrderBackup2017<br>FROM Customers<br>LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;


## Data Transfer Language (DTL) Commands
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
COMMIT | Used to save any transaction into the database permanently.
ROLLBACK | Restores the database to the last committed state.
SAVEPOINT | Creates points within groups of transactions in which to ROLLBACK

SET TRANSACTION Places a name on a transaction

## Clauses
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
CASE | Creates different outputs based on conditions.<br><br>**Note**: If there is no ELSE part and no conditions are true, it returns NULL. | CASE<br>__WHEN condition1 THEN result1<br>__WHEN condition2 THEN result2<br>__WHEN conditionN THEN resultN<br>__ELSE result<br>END; | SELECT OrderID, Quantity,<br>CASE<br>__WHEN Quantity > 30 THEN 'The quantity is greater than 30'<br>__WHEN Quantity = 30 THEN 'The quantity is 30'<br>__ELSE 'The quantity is under 30'<br>END AS QuantityText<br>FROM OrderDetails;<br><br>SELECT CustomerName, City, Country<br>FROM Customers<br>ORDER BY<br>(CASE<br>__WHEN City IS NULL THEN Country<br>__ELSE City<br>END);
FULL (OUTER) JOIN | Returns all records when there is a match in either left or right table.<br><br>**Note**: The FULL OUTER JOIN keyword returns all matching records from both tables whether the other table matches or not. | SELECT column_name(s)<br>FROM table1<br>FULL OUTER JOIN table2<br>ON table1.column_name = table2.column_name<br>WHERE condition; | SELECT<br>Customers.CustomerName, Orders.OrderID<br>FROM Customers<br>FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID<br>ORDER BY Customers.CustomerName;
HAVING | Used instead of WHERE with aggregate functions. <br><br>**Note**: The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions. | SELECT column_name(s)<br>FROM table_name<br>WHERE condition<br>GROUP BY column_name(s)<br>HAVING condition<br>ORDER BY column_name(s); | SELECT COUNT(CustomerID), Country<br>FROM Customers<br>GROUP BY Country<br>HAVING COUNT(CustomerID) > 5;<br><br>SELECT COUNT(CustomerID), Country<br>FROM Customers<br>GROUP BY Country<br>HAVING COUNT(CustomerID) > 5<br>ORDER BY COUNT(CustomerID) DESC;<br><br>SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders<br>FROM (Orders<br>INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)<br>GROUP BY LastName<br>HAVING COUNT(Orders.OrderID) > 10;<br><br>SELECT Employees.LastName, COUNT(Orders.OrderID) AS NumberOfOrders<br>FROM Orders<br>INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID<br>WHERE LastName = 'Davolio' OR LastName = 'Fuller'<br>GROUP BY LastName<br>HAVING COUNT(Orders.OrderID) > 25;
INNER JOIN | Returns records that have matching values in both tables | SELECT column_name(s)<br>FROM table1<br>INNER JOIN table2<br>ON table1.column_name = table2.column_name; | **Find values when the Customers Table belongs to the Orders Table (CustomerID is a foreign key in the Orders Table)**<br>SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate<br>FROM Orders<br>INNER JOIN Customers<br>ON Orders.CustomerID = Customers.CustomerID;<br><br>**Find values when the Customers Table and the Shipper's Table belong to the Orders Table (CustomerID and the ShipperID are foreign keys in the Orders Table)**<br>SELECT Orders.OrderID, Customers.CustomerName, Shippers.ShipperName<br>FROM ((Orders<br>INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID)<br>INNER JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID);
IS NULL | Tests for empty values | SELECT column_names<br>FROM table_name<br>WHERE column_name IS NULL;
IS NOT NULL | Tests for non-empty values | SELECT column_names<br>FROM table_name<br>WHERE column_name IS NOT NULL;
LEFT (OUTER) JOIN | Returns all records from the left table, and the matched records from the right table.<br><br>**Note**: The LEFT JOIN keyword returns all records from the left table (`Customers`), even if there are no matches in the right table (`Orders`). | SELECT column_name(s)<br>FROM table1<br>LEFT JOIN table2<br>ON table1.column_name = table2.column_name; | SELECT Customers.CustomerName, Orders.OrderID<br>FROM Customers<br>LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID<br>ORDER BY Customers.CustomerName;
LIMIT | Specifies the number of records to return in the result set<br><br>**Note**: MySQL and PostgreSQL supports the LIMIT clause | SELECT column_name(s)<br>FROM table_name<br>WHERE condition<br>LIMIT number; | SELECT * FROM Customers<br>WHERE Country='Germany'<br>LIMIT 3;
RIGHT (OUTER) JOIN | Returns all records from the right table, and the matched records from the left table.<br><br>**Note**: The RIGHT JOIN keyword returns all records from the right table (`Employees`), even if there are no matches in the left table (`Orders`). | SELECT column_name(s)<br>FROM table1<br>RIGHT JOIN table2<br>ON table1.column_name = table2.column_name; | SELECT Orders.OrderID, Employees.LastName, Employees.FirstName<br>FROM Orders<br>RIGHT JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID<br>ORDER BY Orders.OrderID;
ROWNUM | Specifies the number of records to return in the result set<br><br>**Note**: Oracle supports the ROWNUM clause | SELECT column_name(s)<br>FROM table_name<br>WHERE ROWNUM <= number; | SELECT * FROM Customers<br>WHERE Country='Germany' AND ROWNUM <= 3;
SELF JOIN | THis is a regular join, but the table is joined with itself. | SELECT column_name(s)<br>FROM table1 T1, table1 T2<br>WHERE condition; | FROM Customers A, Customers B<br>WHERE A.CustomerID <> B.CustomerID<br>AND A.City = B.City<br>ORDER BY A.City;
TOP | Specifies the number of records to return in the result set<br><br>**Note**: MS Access supports the ROWNUM clause | SELECT TOP number`I`percent column_name(s)<br>FROM table_name<br>WHERE condition; | SELECT TOP 3 * FROM Customers<br>WHERE Country='Germany';
WHERE | Filters a result set to include only records that fulfill a specified condition.<br><br>**Note**: SQL requires single quotes around text values (most database systems will also allow double quotes). However, numeric fields should not be enclosed in quotes. | SELECT column1, column2, ...<br>FROM table_name<br>WHERE condition; | SELECT * FROM Customers<br>WHERE Country='Mexico';<br><br>SELECT * FROM Customers<br>WHERE CustomerID=1;<br><br>SELECT * FROM Customers<br>WHERE Date='2014-04-23';

## Functions
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
AVG() | Returns the average value of a numeric column.<br><br>**Note**: NULL values are ignored. | SELECT AVG(column_name)<br>FROM table_name<br>WHERE condition; | SELECT AVG(Price)<br>FROM Products;
COALESCE() | Returns an alternative value if an expression is NULL.<br><br>**Note**: MySQL and PostgreSQL supports the COALESCE() function |  | SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))<br>FROM Products;
COUNT() | Returns the number of rows that matches a specified criteria.<br><br>**Note**: NULL values are not counted. | SELECT COUNT(column_name)<br>FROM table_name<br>WHERE condition; | SELECT COUNT(ProductID)<br>FROM Products;
IFNULL() | Returns an alternative value if an expression is NULL.<br><br>**Note**: MySQL and PostgreSQL supports the IFNULL() function |  | <br>SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))<br>FROM Products;
ISNULL() | Returns an alternative value when an expression is NULL.<br><br>**Note**: SQL Server supports the ISNULL() function. | | SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))<br>FROM Products;
MAX() | Returns the largest value of the selected column. | SELECT MAX(column_name)<br>FROM table_name<br>WHERE condition; | SELECT MAX(Price) AS LargestPrice<br>FROM Products;
MIN() | Returns the smallest value of the selected column. | SELECT MIN(column_name)<br>FROM table_name<br>WHERE condition; | SELECT MIN(Price) AS SmallestPrice<br>FROM Products;
NVL() | Returns an alternative value if an expression is NULL.<br><br>**Note**: Oracle supports the NVL() function | | SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))<br>FROM Products;
SUM() | Returns the total sum of a numeric column. | SELECT SUM(column_name)<br>FROM table_name<br>WHERE condition; | SELECT SUM(Quantity)<br>FROM OrderDetails;

## Operators
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
ALL | Returns true if all of the subquery values meet the condition. **Note**: The ALL operator returns true if all of the subquery values meet the condition. | SELECT column_name(s)<br>FROM table_name<br>WHERE column_name operator ALL (SELECT column_name FROM table_name WHERE condition); | SELECT ProductName<br>FROM Products<br>WHERE ProductID = ALL (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);
AND | Only includes rows where both conditions is true | SELECT column1, column2, ...<br>FROM table_name<br>WHERE condition1 AND condition2...;| SELECT * FROM Customers<br>WHERE Country='Germany' AND City='Berlin';
ANY | Returns true if any of the subquery values meet the condition.<br><br>**Note**:The ANY operator returns true if any of the subquery values meet the condition. | SELECT column_name(s)<br>FROM table_name<br>WHERE column_name operator ANY<br>(SELECT column_name FROM table_name WHERE condition); | SELECT ProductName<br>FROM Products<br>WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity = 10);<br><br>SELECT ProductName<br>FROM Products<br>WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity > 99);
AS | Renames a column or table with an alias.<br><br>**Note**:SQL aliases are used to give a table, or a column in a table, a temporary name. Aliases are often used to make column names more readable. An alias only exists for the duration of the query. | **Alias Column Syntax**<br>SELECT column_name AS alias_name<br>FROM table_name;<br><br>**Alias Table Syntax**<br>SELECT column_name(s)<br>FROM table_name AS alias_name; | **Alias for Columns Examples**<br>SELECT CustomerID AS ID, CustomerName AS Customer<br>FROM Customers;<br><br>**Alias for Tables Example**<br>SELECT o.OrderID, o.OrderDate, c.CustomerName<br>FROM Customers AS c, Orders AS o<br>WHERE c.CustomerName='Around the Horn' AND c.CustomerID=o.CustomerID;
BETWEEN | Selects values within a given range | SELECT column_name(s)<br>FROM table_name<br>WHERE column_name BETWEEN value1 AND value2; | SELECT * FROM Products<br>WHERE Price BETWEEN '2018-10-02' AND '2020-04-26';<br><br>SELECT * FROM Products<br>WHERE Price NOT BETWEEN 10 AND 20;<br><br>SELECT * FROM Products<br>WHERE Price BETWEEN 10 AND 20<br>AND CategoryID NOT IN (1,2,3);
EXISTS | Tests for the existence of any record in a subquery.<br><br>**Note**: The EXISTS operator returns true if the subquery returns one or more records. | SELECT column_name(s)<br>FROM table_name<br>WHERE EXISTS<br>(SELECT column_name FROM table_name WHERE condition); | SELECT SupplierName<br>FROM Suppliers<br>WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price < 20);<br><br>SELECT SupplierName<br>FROM Suppliers<br>WHERE EXISTS (SELECT ProductName FROM Products WHERE Products.SupplierID = Suppliers.supplierID AND Price = 22);
IN | Allows you to specify multiple values in a WHERE clause | SELECT column_name(s)<br>FROM table_name<br>WHERE column_name IN (value1, value2, ...); | SELECT * FROM Customers<br>WHERE Country IN ('Germany', 'France', 'UK');<br><br>SELECT * FROM Customers<br>WHERE Country NOT IN ('Germany', 'France', 'UK');
LIKE | Searches for a specified pattern in a column. | SELECT column1, column2, ...<br>FROM table_name<br>WHERE columnN LIKE pattern; | **Finds values that start with "a"**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE 'a%';<br><br>**Finds values that end with "a"**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '%a';<br><br>**Finds values that have "or" in any position**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '%or%';<br><br>**Finds values that have "r" in the second position**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '_r%';<br><br>**Finds values that start with "a" and ends with "o"**<br>SELECT * FROM Customers<br>WHERE ContactName LIKE 'a%o';<br><br>**Finds values starting with "L", followed by any character, followed by "n", followed by any character, followed by "on"**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE 'L_n_on';<br><br>**Finds values that start with "b", "s", or "p"**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '[bsp]%';<br><br>**Finds values that start with "a", "b", or "c":**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '[a-c]%';<br><br>**Finds values that does NOT start with "a"**<br>SELECT * FROM Customers<br>WHERE CustomerName NOT LIKE 'a%';<br><br>**Finds values that does NOT start with "bsp"**<br>SELECT * FROM Customers<br>WHERE CustomerName LIKE '[!bsp]%';
NOT | Only includes rows where a condition is not true | SELECT column1, column2, ...<br>FROM table_name<br>WHERE NOT condition; | SELECT * FROM Customers<br>WHERE NOT Country='Germany';<br><br>SELECT * FROM Customers<br>WHERE NOT Country='Germany' AND NOT Country='USA';
OR | Includes rows where either condition is true | SELECT column1, column2, ...<br>FROM table_name<br>WHERE condition1 OR condition2 ...; | SELECT * FROM Customers<br>WHERE Country='Germany' AND (City='Berlin' OR City='München');
UNION | Combines the result set of two or more SELECT statements. <br><br>**Note**: Only distinct values | SELECT column_name(s) <br>FROM table1<br>UNION<br>SELECT column_name(s) FROM table2; | SELECT City FROM Customers<br>UNION<br>SELECT City FROM Suppliers<br>ORDER BY City;<br><br>SELECT City, Country FROM Customers<br>WHERE Country='Germany'<br>UNION<br>SELECT City, Country FROM Suppliers<br>WHERE Country='Germany'<br>ORDER BY City;<br><br>SELECT 'Customer' As Type, ContactName, City, Country<br>FROM Customers<br>UNION<br>SELECT 'Supplier', ContactName, City, Country<br>FROM Suppliers;<br><br>SELECT 'Customer' As Type, ContactName, City, Country<br>FROM Customers<br>UNION<br>SELECT 'Supplier', ContactName, City, Country<br>FROM Suppliers;
UNION ALL | Combines the result set of two or more SELECT statements. <br><br>**Note**: Allows duplicate values | SELECT column_name(s) <br>FROM table1<br>UNION ALL<br>SELECT column_name(s) FROM table2; | SELECT City FROM Customers<br>UNION ALL<br>SELECT City FROM Suppliers<br>ORDER BY City;<br><br>SELECT City, Country FROM Customers<br>WHERE Country='Germany'<br>UNION ALL<br>SELECT City, Country FROM Suppliers<br>WHERE Country='Germany'<br>ORDER BY City;

## Other Operators
Operator | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
`=` | Equal
`>` | Greater than
`<` | Less than
`>=` | Greater than or equal
`<=` | Less than or equal
`<>` OR `!=` | Not equal

## Sorting
Command | Description | Example(s) | Illustration(s)
------------ | ------------- | ------------- | -------------
GROUP | Groups the result set (used with aggregate functions: COUNT, MAX, MIN, SUM, AVG) | SELECT column_name(s)<br>FROM table_name<br>WHERE condition<br>GROUP BY column_name(s)<br>ORDER BY column_name(s); | SELECT COUNT(CustomerID), Country<br>FROM Customers<br>GROUP BY Country;<br><br>SELECT COUNT(CustomerID), Country<br>FROM Customers<br>GROUP BY Country<br>ORDER BY COUNT(CustomerID) DESC;<br><br>SELECT Shippers.ShipperName, COUNT(Orders.OrderID) AS NumberOfOrders FROM Orders<br>LEFT JOIN Shippers ON Orders.ShipperID = Shippers.ShipperID<br>GROUP BY ShipperName;
ORDER | Sorts the result set in ascending or descending order | SELECT column1, column2, ...<br>FROM table_name<br>ORDER BY column1, column2, ...<br>ASC`I`DESC; | **Order by Single Column**<br>SELECT * FROM Customers<br>ORDER BY Country;<br><br>**Order by Single Column**<br>SELECT * FROM Customers<br>ORDER BY Country DESC;<br><br>**Order by Several Columns**<br>SELECT * FROM Customers<br>ORDER BY Country, CustomerName;<br><br>**Order by Several Columns**<br>SELECT * FROM Customers<br>ORDER BY Country ASC, CustomerName DESC;

## Resources
1. [W3 Schools SQL Tutorial](https://www.w3schools.com/sql/default.asp)
2. [SQL Cheat Sheet](https://hackr.io/blog/sql-cheat-sheet)
