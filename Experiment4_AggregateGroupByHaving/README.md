# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
```
How many patients are there in each city?

Sample table: Patients Table
For example:

Result
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3
```
```
select Address,count(*) as TotalPatients
from Patients
group by Address;
```

**Output:**

![image](https://github.com/user-attachments/assets/9f5ef6f0-9a67-4d34-be9c-fd4465520670)


**Question 2**
```
How many medical records are there for each patient?

Sample table:MedicalRecords Table
For example:

Result
PatientID   TotalRecords
----------  ------------
4           4
5           1
6           1
7           1
8           1
10          2

```
code:
```
select PatientID ,count(*) as TotalRecords
from MedicalRecords
group by PatientID;
```
**Output:**

![image](https://github.com/user-attachments/assets/e30c94d2-1756-4e52-8a27-a3cbf2269313)


**Question 3**
```
How many medical records were created in each month?

Sample table:MedicalRecords Table
For example:

Result
Month       TotalRecords
----------  ------------
2023-12     2
2024-01     6
2024-02     2
```
sql code:
```
select strftime('%Y-%m',Date)as Month,count(*) as TotalRecords
from MedicalRecords
group by Month 
order by Month;
```

**Output:**

![image](https://github.com/user-attachments/assets/d940d929-1e6f-4aae-92ad-c84e8e8ba9a4)


**Question 4**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee


id      name    age     address     salary

1       Paul    32      California  20000

4       Mark    25      Richtown    65000

5       David   27       Texas      85000
 

For example:

Result
COUNT
----------
5


```sql
select COUNT(id) as 
COUNT  from employee
where age>32;
```

**Output:**

![WhatsApp Image 2025-04-30 at 08 42 14_6dce328f](https://github.com/user-attachments/assets/32edb697-412f-43a3-930b-61aa443b0739)

**Question 5**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
price_diff
----------
4.65

```sql
select max(price) - min(price) as price_diff
from fruits ;
```

**Output:**
![WhatsApp Image 2025-04-30 at 08 42 14_4c71ca1f](https://github.com/user-attachments/assets/c4b9e506-481c-4135-8ce6-de1163261088)


**Question 6**
---
-- Paste Question 6 here

```sql
-- Paste your SQL code below for Question 6
```

**Output:**

![Output6](output.png)

**Question 7**
---
-- Paste Question 7 here

```sql
-- Paste your SQL code below for Question 7
```

**Output:**

![Output7](output.png)

**Question 8**
---
-- Paste Question 8 here

```sql
-- Paste your SQL code below for Question 8
```

**Output:**

![Output8](output.png)

**Question 9**
---
-- Paste Question 9 here

```sql
-- Paste your SQL code below for Question 9
```

**Output:**

![Output9](output.png)

**Question 10**
---
-- Paste Question 10 here

```sql
-- Paste your SQL code below for Question 10
```

**Output:**

![Output10](output.png)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
