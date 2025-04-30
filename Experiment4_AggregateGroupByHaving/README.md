# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- *MIN()* – Smallest value  
- *MAX()* – Largest value  
- *COUNT()* – Number of rows  
- *SUM()* – Total of values  
- *AVG()* – Average of values

*Syntax:*
sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;

### GROUP BY
Groups records with the same values in specified columns.
*Syntax:*
sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;

### HAVING
Filters the grouped records based on aggregate conditions.
*Syntax:*
sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;


*Question 1*
--
What is the most common diagnosis among patients?

Sample table:MedicalRecords Table
![image](https://github.com/user-attachments/assets/cb144231-d755-4408-8202-dafa08d37bd2)

sql
SELECT Diagnosis,
   COUNT(*) AS DiagnosisCount
FROM MedicalRecords
GROUP BY Diagnosis
ORDER BY DiagnosisCount DESC
LIMIT 1;


*Output:*

![image](https://github.com/user-attachments/assets/3e67036d-281d-4c20-b19d-bafba7f96563)

*Question 2*
---
How many appointments are scheduled for each patient?

Sample table: Appointments Table

name                  type
--------------------  ----------
AppointmentID         INTEGER
PatientID             INTEGER
DoctorID              INTEGER
AppointmentDateTime   DATETIME
Purpose               TEXT
Status                TEXT


sql
SELECT PatientID,
COUNT(*) AS TotalAppointments
FROM Appointments
GROUP BY PatientID;


*Output:*

![image](https://github.com/user-attachments/assets/acf11c5d-88ef-4213-989e-45badd33f6a8)

*Question 3*
---
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT


sql
SELECT strftime('%Y',ValidityPeriod) AS ValidityYear,
COUNT(DISTINCT PatientID) AS TotalPatients
FROM Insurance
GROUP BY ValidityYear;


*Output:*

![image](https://github.com/user-attachments/assets/de728464-fb3c-4fbf-b700-b459d7f12fc2)

*Question 4*
---
Write a SQL query to find  how many employees work in California?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER


sql
SELECT 
COUNT(*) AS employees_in_california
FROM employee
WHERE city = 'California';


*Output:*

![image](https://github.com/user-attachments/assets/4483a528-2f11-417e-b41c-bb8c621da50d)

*Question 5*
---
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER


sql
SELECT COUNT(DISTINCT city)
AS unique_cities
FROM customer;


*Output:*

![image](https://github.com/user-attachments/assets/609b436e-5b83-4848-9b09-d7c34fdb5edb)

*Question 6*
---
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 
Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL


sql
SELECT SUM(inventory) 
AS total_available_amount 
FROM fruits
WHERE price > 0.5;


*Output:*

![image](https://github.com/user-attachments/assets/4e2baf2c-03c1-478e-ab96-78bb52bdf718)

*Question 7*
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER


sql
SELECT name AS Employee_Name,
age AS Age
FROM employee
ORDER BY age ASC
LIMIT 1;



*Output:*

![image](https://github.com/user-attachments/assets/f795fa76-00d4-4910-9486-0fa8eed5b3f0)

*Question 8*
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products
![image](https://github.com/user-attachments/assets/d31e75af-762b-4bc9-b695-a4801d30f3e4)

sql
SELECT category_id,
COUNT(product_name) AS 'count(product_name)'
FROM products
WHERE category_id < 3
GROUP BY category_id;


*Output:*

![image](https://github.com/user-attachments/assets/9f3ddca8-edb6-471c-ae5c-1a5d0866895c)

*Question 9*
---
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.

Table: customer1
![image](https://github.com/user-attachments/assets/1bb42ba1-861f-4a2e-85fb-996909595b8e)

sql
SELECT 
(age/5) * 5 AS age_group,
MIN(salary) AS 'MIN(salary)'
FROM customer1
GROUP BY (age / 5) * 5
HAVING MIN(salary) < 2000


*Output:*

![image](https://github.com/user-attachments/assets/0c8b928d-ecfa-4d41-bcd8-d02bd6d54349)

*Question 10*
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Sample table: employee1
![image](https://github.com/user-attachments/assets/94c39ded-93b2-444c-b087-ee607c875d49)

 sql
SELECT jdate,
   SUM(workhour) AS 'SUM(workhour)'
FROM employee1
GROUP BY jdate
HAVING SUM(workhour) > 40
ORDER BY jdate;


*Output:*

![image](https://github.com/user-attachments/assets/76bdd1a0-44a9-4517-944f-135e00bc50a7)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
