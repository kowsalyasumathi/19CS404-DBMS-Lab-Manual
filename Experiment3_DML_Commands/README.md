# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```

*Question 1*
--
```
Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

Products Table 

name          type       
----------    ---------- 
product_id     INT PRIMARY KEY        
product_name   VARCHAR(10) 
category       VARCHAR(50) 
cost_price     DECIMAL(10) 
sell_price     DECIMAL(10) 
reorder_lv     INT        
quantity       INT        
supplier_id    INT           
For example:

Test	Result
select changes();
changes()
----------
4
```
sql code
```
update products
set sell_price=sell_price*1.15
where quantity <50 and
supplier_id =10;
```
*Output:*

![Screenshot (219)(1)](https://github.com/user-attachments/assets/ea2daf48-c7c8-4587-b7b2-4acb6ae2b9a3)

*Question 2*
---
```
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.

products table

---------------
product_id
product_name
category_id
availability
```
SQL CODE 
```
update products
set product_name='Grapefruit'
where product_id =4;
```
*Output:*

![Screenshot (220)(1)](https://github.com/user-attachments/assets/70e9f398-fe6f-4790-a6e8-579e7afbc95a)


*Question 3*
---
```
For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
1
```
SQL CODE 
```
update sales
set sell_price=sell_price+3
where product_id in (select product_id from products
where supplier_id=4);
```

*Output:*

![Screenshot (221)(1)](https://github.com/user-attachments/assets/d33e294d-51d4-43a1-9b00-03ab1494ce31)


*Question 4*
---
```
Write a SQL statement to Update the grade of all customers in Chennai city as  5. 

Customer table (customer_id,cust_name,city,grade,salesman_id)
```
SQL CODE
```
update customer
set grade=5
where city='Chennai';
```

*Output:*

![Screenshot (222)(1)](https://github.com/user-attachments/assets/9f6f0708-60c6-45df-90b0-a6bf9452c548)


*Question 5*
```
Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
3
```
SQL CODE 
```
update sales
set total_sell_price=sell_price*quantity
where product_id=10;
```
*Output:*
![Screenshot (223)(1)](https://github.com/user-attachments/assets/e1f98b9d-1c58-45bf-9ef4-1014a2d4b5ce)

*Question 6*
---
```
Write a SQL query to find all those customers who does not have any grade. Return customer_id, cust_name, city, grade, salesman_id.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
For example:

Result
customer_id  cust_name    city        grade       salesman_id
-----------  -----------  ----------  ----------  -----------
1            John Mathew  New York                5000
2            Michel John  Paris                   2000
 
```
SQL CODE
```
select customer_id,cust_name,city,grade,salesman_id 
from customer 
where grade is null;
```

*Output:*
![Screenshot (226)(1)](https://github.com/user-attachments/assets/4695bf02-3dcb-4dcf-87bb-46339ceab3d8)


*Question 7*
---
```
Write a SQL query to Delete All Doctors with a NULL Last Name

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
For example:

Test	Result
SELECT * FROM doctors;
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics
4           Febin                   Cardiology
doctor_id   first_name  last_name   specialization
----------  ----------  ----------  --------------
1           John        Smith       Cardiology
2           Emily       Johnson     Orthopedics
3           Michael     Brown       Pediatrics

```
SQL CODE
```
delete from doctors
where last_name is null;
```

*Output:*

![Screenshot (224)(1)](https://github.com/user-attachments/assets/86932326-4a4b-42ae-a3b5-00438adf82ed)


*Question 8*
---
```
Write a SQL query to Delete a Specific Surgery whose ID is 3

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date
For example:

Test	Result
SELECT * FROM surgeries;
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
3           3           3           2024-03-25
surgery_id  patient_id  surgeon_id  surgery_date
----------  ----------  ----------  ------------
1           1           1           2024-01-15
2           2           2           2024-02-28
```
SQL CODE 
```
delete from surgeries
where surgery_id=3;
```

*Output:*

![Screenshot (225)(1)](https://github.com/user-attachments/assets/4f1e5ef4-eb06-47ed-9ddb-db788e49ccd5)

*Question 9*
---
```
Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.
- Sample table: Doctors
- attributes : doctor_id, first_name, last_name, specialization
```
SQL CODE
```
DELETE FROM Doctors
WHERE specialization IN ('Pediatrics','Cardiology')
AND last_name = 'Brown';
```

*Output:*

![image](https://github.com/user-attachments/assets/1e39da2b-7c39-4ec5-81a5-16ca8ae1dc61)

*Question 10*
---
```
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |
```
SQL CODE
```
DELETE FROM Customer
WHERE CUST_NAME LIKE 'M%'
AND PAYMENT_AMT < 3000;
```

*Output:*

![image](https://github.com/user-attachments/assets/44ecc6fe-d922-4951-b39a-205a7078663a)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
