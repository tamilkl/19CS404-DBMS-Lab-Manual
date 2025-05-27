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
*Steps:*
- Create two tables: employees (for storing data) and employee_log (for logging the inserts).
- Write an *AFTER INSERT* trigger on the employees table to log the new data into the employee_log table.

*PL/SQL query:*

create table employees11(
 employee_id INT primary key,
 first_name VARCHAR(50),
 dept_no INT,
 salary DECIMAL(10,2)
 );
 create table employee_log(
   log_id INT AUTO_INCREMENT primary key,
   employee_id INT,
   first_name VARCHAR(50),
   dept_no INT,
   salary DECIMAL(10,2),
   log_timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   DELIMITER $$
   create trigger trg_log_employee_insert
   AFTER INSERT ON employees11
   FOR EACH ROW
   BEGIN
      Insert into employee_log(employee_id,first_name,dept_no,salary)
      values(New.employee_id,new.first_name,new.dept_no,new.salary);
  END$$
  DELIMITER ;
  INSERT INTO employees11(employee_id,first_name,dept_no,salary)
  values(1,'Alice',10,5000.00);
  select * from employee_log;

*Expected Output:*
- A new entry is added to the employee_log table each time a new record is inserted into the employees table.

*Output:*

![image](https://github.com/user-attachments/assets/7d12feda-20aa-4c84-b1c8-e24a246ca428)

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
*Steps:*
- Write a *BEFORE DELETE* trigger on the sensitive_data table.
- Use RAISE_APPLICATION_ERROR to prevent deletion and issue a custom error message.

*PL/SQL query:*

create table sensitive_data(
    record_id INT primary key,
    info varchar(50)
    );
    DELIMITER $$
    create trigger trg_prevent_delete_sensitive
    BEFORE delete on sensitive_data
    FOR EACH ROW
    BEGIN
      SIGNAL SQLSTATE '45000'
      SET MESSAGE_TExT = 'ERROR:DELETION not allowed in this table';
END$$
DELIMITER ;
Insert INTO sensitive_data(record_id,info) values (1,'Top secret');
DELETE FROM sensitive_data where record_id=1;


*Expected Output:*
- If an attempt is made to delete a record from sensitive_data, an error message is raised, e.g., ERROR: Deletion not allowed on this table.

*Output:*

![image](https://github.com/user-attachments/assets/f08d5c42-35d1-4210-be6c-f5261c319a91)

---

## 3. Write a trigger to automatically update a last_modified timestamp.
*Steps:*
- Add a last_modified column to the products table.
- Write a *BEFORE UPDATE* trigger on the products table to set the last_modified column to the current timestamp whenever an update occurs.

*PL/SQL query:*

CREATE TABLE products 
(
    product_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    price NUMERIC(10, 2),
    stock_quantity INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    last_modified TIMESTAMP
);
DELIMITER $$

    CREATE TRIGGER trg_set_last_modified
    BEFORE UPDATE ON products
    FOR EACH ROW
    BEGIN
        SET NEW.last_modified = CURRENT_TIMESTAMP;
    END$$

DELIMITER ;

INSERT INTO products (name, description, price, stock_quantity)
VALUES 
('Wireless Mouse', 'Ergonomic wireless mouse with USB receiver', 25.99, 100),
('Mechanical Keyboard', 'RGB backlit mechanical keyboard', 59.99, 50),
('HD Monitor', '24-inch Full HD LED monitor', 149.99, 30);

UPDATE products SET price = 27.99 WHERE product_id = 1;
UPDATE products SET name = 'Key Board '  WHERE product_id = 2;
UPDATE products SET stock_quantity = 40 WHERE product_id = 3;

SELECT product_id, name, created_at, last_modified FROM products;

*Expected Output:*
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

*Output:*
Before Updating the record:

![image](https://github.com/user-attachments/assets/abd98efa-fe08-4cbc-8434-8ea886c3360f)

After updating the record:

![image](https://github.com/user-attachments/assets/490136a2-5eaf-4419-937a-a0b7b89d8e10)


---

## 4. Write a trigger to keep track of the number of updates made to a table.
*Steps:*
- Create an audit_log table with a counter column.
- Write an *AFTER UPDATE* trigger on the customer_orders table to increment the counter in the audit_log table every time a record is updated.

*PL/SQL query:*

CREATE TABLE customer_orders (
order_id INT PRIMARY KEY,
customer_name VARCHAR(100),
order_amount DECIMAL(10,2)
);
CREATE TABLE audit_log (
id INT PRIMARY KEY,
update_count INT DEFAULT 0
);
INSERT INTO audit_log (id, update_count) VALUES (1,0);
DELIMITER $$
CREATE TRIGGER trg_track_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
UPDATE audit_log
SET update_count = update_count + 1
WHERE id = 1;
END$$
DELIMITER ;
INSERT INTO customer_orders(order_id,customer_name,order_amount)
values(100,'Doe',150.00);
UPDATE customer_orders
SET order_amount = 200.00
WHERE order_id = 100;
UPDATE customer_orders
SET order_amount = 400.00
WHERE order_id = 100;
SELECT * FROM audit_log;


*Expected Output:*
- The audit_log table will maintain a count of how many updates have been made to the customer_orders table.

*Output:*

![image](https://github.com/user-attachments/assets/100fd565-cd55-497c-98c5-422fd1603a75)

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
*Steps:*
- Write a *BEFORE INSERT* trigger on the employees table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

*PL/SQL query:*

CREATE TABLE employee6 
(
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    dept_no INT,
    salary DECIMAL(10,2)
);

DELIMITER $$

        CREATE TRIGGER trg_check_salary_before_insert2
        BEFORE INSERT ON employee6
        FOR EACH ROW
        BEGIN
            IF NEW.salary < 3000 THEN
                SIGNAL SQLSTATE '45000'
                SET MESSAGE_TEXT = 'ERROR: Salary Below Minimum Threshold.';
            END IF;
        END$$

DELIMITER ;

INSERT INTO employee6(employee_id, first_name, dept_no, salary) VALUES (1, 'Bob', 20, 299.00);


*Expected Output:*
- If the inserted salary in the employees table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: ERROR: Salary below minimum threshold.

*Output:*

If the inserted salary in the employees table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: ERROR: Salary below minimum threshold.

![image](https://github.com/user-attachments/assets/e5006bf2-1b29-4d82-b409-3e7fb47582ab)


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

