# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

*Syntax:*
sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);

### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
sql
ALTER TABLE std ADD (Address CHAR(10));

(b) MODIFY
sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));

(c) DROP
sql
ALTER TABLE relation_name DROP COLUMN field_name;

(d) RENAME
sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;

### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
sql
DROP TABLE relation_name;

### 4. RENAME
Used to rename an existing database object.
sql
RENAME TABLE old_relation_name TO new_relation_name;

### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);

### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);

### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);

### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);

### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);

### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);


*Question 1*
--
```
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test
INSERT INTO Shipments (ShipmentID, ShipmentDate, SupplierID, OrderID) VALUES (2, '2024-08-03', 99, 1);
Result:
Error: FOREIGN KEY constraint failed
```
SQL CODE
```
create table Shipments(
ShipmentID  INTEGER  primary key,
ShipmentDate  DATE,
SupplierID  INTEGER,
OrderID INTEGER,
foreign key (SupplierID) references Suppliers(SupplierID),
foreign key (OrderID) references Orders(OrderID));
```

*Output:*

![Screenshot (209)(1)](https://github.com/user-attachments/assets/4a0bfe31-8f0c-484c-b1fa-c38a31e78383)


*Question 2*
---
```
Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
DueDate as DATE should be greater than the InvoiceDate.
Amount as REAL should be greater than 0.
For example:

Test
INSERT INTO Invoices (InvoiceID, InvoiceDate)
VALUES (1, '2024-08-08'),(1,'2024-09-08');
Result
Error: UNIQUE constraint failed: Invoices.InvoiceID
```
SQL CODE
```
create table Invoices(
InvoiceID  INTEGER  primary key,
InvoiceDate  DATE,
DueDate  DATE check (DueDate>InvoiceDate),
Amount  REAL check(Amount>0));
```

*Output:*

![Screenshot (210)(1)](https://github.com/user-attachments/assets/beb4f590-0319-44e8-a58a-43c0904a30a9)


*Question 3*
---
```Write a SQL query to add birth_date attribute as timestamp (datatype) in the table customer 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
 

For example:

Test	Result
pragma table_info('customer');
cid         name         type                               notnull     dflt_value  pk
----------  -----------  ---------------------------------  ----------  ----------  ----------
0           customer_id  integer primarykey auto increment  0                       0
1           cust_name    varchar2(30)                       0                       0
2           city         varchar(30)                        0                       0
3           grade        number                             0                       0
4           salesman_id  number                             0                       0
5           birth_date   timestamp                          0                       0
```
SQL CODE
```
alter table customer 
add column birth_date  timestamp;
);
```
*Output:*

![Screenshot (211)(1)](https://github.com/user-attachments/assets/ce9264f2-a072-41a0-88ca-9c5ec231ba95)

*Question 4*
---
```
Insert all customers from Old_customers into Customers

Table attributes are CustomerID, Name, Address, Email

For example:

Test	Result
select * from Customers;
CustomerID  Name             Address         Email
----------  ---------------  --------------  ---------------------
301         Michael Johnson  123 Elm Street  michael.j@example.com
302         Sarah Lee        456 Oak Avenue  sarah.lee@example.com
303         David Wilson     789 Pine Road   david.w@example.com

```
SQL CODE
```
insert into Customers(CustomerID,Name,Address,Email)
select * from Old_customers;
```
*Output:*

![Screenshot (212)(1)](https://github.com/user-attachments/assets/70cc7585-d735-427e-b009-7aa3e289b88c)

*Question 5*
---
```
Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.
For example:

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed
```
SQL CODE
```
create table  ProjectAssignments(
AssignmentID  INTEGER  primary key,
EmployeeID  INTEGER,
ProjectID  INTEGER,
AssignmentDate  DATE  NOT NULL,
foreign key (EmployeeID) references Employees(EmployeeID),
foreign key (ProjectID) references Projects(ProjectID));
```


*Output:*

![Screenshot (213)(1)](https://github.com/user-attachments/assets/479030b6-6017-441e-bf81-65698bed593b)


*Question 6*
---
```
Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           Country     TEXT        0                       0

```
SQL CODE
```
alter table Student_details
add column Country  TEXT;
);
```

*Output:*

![Screenshot (214)(1)](https://github.com/user-attachments/assets/c5a68b60-8a31-4ac6-beee-fd99b0a21356)


*Question 7*
---
```
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
 
 
For example:

Test	Result
SELECT ISBN, Title, Author
FROM Books 


ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

```
SQL CODE
```
insert into Books(ISBN,Title,Author)
values('978-6655443321','Big Data Analytics','Karen Adams');
```
*Output:*
![Screenshot (215)(1)](https://github.com/user-attachments/assets/a14f309b-e7fb-4ae2-a6d6-01db6811ac65)


*Question 8*
---
```
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER
For example:

Test	Result
pragma table_info('Orders');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     OrderID     INTEGER     0                       0
1     OrderDate   TEXT        0                       0
2     CustomerID  INTEGER     0                       0

```
SQL CODE
```
create table Orders(
OrderID  INTEGER,
OrderDate TEXT,
CustomerID  INTEGER);
```

*Output:*

![Screenshot (216)(1)](https://github.com/user-attachments/assets/d78efde8-096f-4563-a231-4b9029b1aec8)


*Question 9*
---
```
In the Cusomers table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

CustomerID  Name          Address      City        ZipCode
----------  ------------  ----------   ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Manor  Gotham      10007
308         Peter Parker  Queens                   11375
 

For example:

Test	Result
SELECT * FROM Customers;
CustomerID  Name          Address     City        ZipCode
----------  ------------  ----------  ----------  ----------
306         Diana Prince  Themyscira
307         Bruce Wayne   Wayne Mano  Gotham      10007
308         Peter Parker  Queens                  11375

```
SQL CODE
```
insert into Customers(CustomerID,Name,Address,City,ZipCode)
values('306','Diana Prince','Themyscira','',''),
('307','Bruce Wayne','Wayne Mano','Gotham','10007'),
('308','Peter Parker','Queens','','11375');
```


*Output:*

![Screenshot (217)(1)](https://github.com/user-attachments/assets/4d425c5d-eef5-46af-9e54-e9ddfb6802b0)


*Question 10*
---
```
Create a table named Attendance with the following constraints:
AttendanceID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
AttendanceDate as DATE.
Status as TEXT should be one of 'Present', 'Absent', 'Leave'.
For example:

Test	Result
INSERT INTO Attendance (AttendanceID, EmployeeID, AttendanceDate, Status) VALUES (1, 1, '2024-08-01', 'Present');
SELECT * FROM Attendance;
AttendanceID  EmployeeID  AttendanceDate  Status
------------  ----------  --------------  ----------
1             1           2024-08-01      Present
```
SQL CODE
```
create table Attendance(
AttendanceID  INTEGER  primary key,
EmployeeID  INTEGER,
AttendanceDate  DATE,
Status  TEXT  check(status in('Present', 'Absent', 'Leave')),
foreign key (EmployeeID) references Employees(EmployeeID));
```


*Output:*

![Screenshot (218)(1)](https://github.com/user-attachments/assets/fee135b9-58bd-4a52-b6d1-87cafbfefabd)

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
