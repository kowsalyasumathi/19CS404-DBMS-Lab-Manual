# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

---
PROGRAM:
```
CREATE OR REPLACE TRIGGER trg_after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, name, position, salary)
    VALUES (:NEW.emp_id, :NEW.name, :NEW.position, :NEW.salary);
END;
/
SELECT table_name FROM user_tables WHERE table_name IN ('EMPLOYEES', 'EMPLOYEE_LOG');
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    name VARCHAR2(100),
    position VARCHAR2(100),
    salary NUMBER(10, 2)
);
CREATE OR REPLACE TRIGGER trg_after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, name, position, salary)
    VALUES (:NEW.emp_id, :NEW.name, :NEW.position, :NEW.salary);
END;
/
INSERT INTO employees (emp_id, name, position, salary)
VALUES (1, 'Alice', 'Engineer', 75000);
SELECT * FROM employee_log;
```

OUTPUT:

![444616595-92e723aa-0d64-4856-b645-777d1f89c30e](https://github.com/user-attachments/assets/6a03046f-ce6e-46e0-8967-cd754ccc427a)


## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

---
PROGRAM:
```
CREATE OR REPLACE TRIGGER prevent_sensitive_data_deletion
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'Deletion not allowed on this table.');
END;
```
OUTPUT:
![444616885-8271f69f-fd86-4109-9837-4792df93aee8](https://github.com/user-attachments/assets/ae4502bf-56dd-4530-87b0-4bc5a073f1ef)


## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

---
PROGRAM:
```

CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(255),
    -- other columns...
    last_modified TIMESTAMP
);
CREATE OR REPLACE TRIGGER update_products_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/
```
OUTPUT:

![444617144-81355fc0-f468-4ef3-b5c3-b575edc267a3](https://github.com/user-attachments/assets/dfb44a3b-e7f1-46ec-abce-5b6cb05850dd)


## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---
PROGRAM:

```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_id NUMBER,
    order_date DATE,
    order_total NUMBER,
    -- Add other relevant columns as needed
    order_status VARCHAR2(20) -- Added a sample column
);
CREATE TABLE audit_log (
    table_name VARCHAR2(255),
    update_count NUMBER
);

INSERT INTO audit_log (table_name, update_count) VALUES ('customer_orders', 0);
CREATE OR REPLACE TRIGGER customer_orders_update_audit
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'customer_orders';
END;
/
UPDATE customer_orders SET order_status = 'Shipped' WHERE order_id = 1;
SELECT update_count FROM audit_log WHERE table_name = 'customer_orders';
```
OUTPUT:

![444617412-6b8ffbaf-9665-4a71-bdee-815ff87ab536](https://github.com/user-attachments/assets/fd532ffd-bffa-4419-a9ad-0a58942266c3)


## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

PROGRAM:
```

INSERT INTO audit_log (table_name, update_count) VALUES ('customer_orders', 0);
CREATE OR REPLACE TRIGGER customer_orders_update_audit
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'customer_orders';
END;
/
CREATE OR REPLACE TRIGGER check_employee_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'Salary below minimum threshold.');
    END IF;
END;
/
INSERT INTO employees (employee_id, employee_name, salary) VALUES (1, 'Alice Smith', 3500);
INSERT INTO employees (employee_id, employee_name, salary) VALUES (2, 'Bob Johnson', 2500);
SELECT * from employees;
```
OUTPUT:
![444617635-0c3f7cfc-4ebc-4375-8758-778345950e22](https://github.com/user-attachments/assets/dda6d6a7-75ba-4b41-9284-94cce9b06ef8)


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
