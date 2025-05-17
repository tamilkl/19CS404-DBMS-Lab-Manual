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
**Question 1**

Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

![image](https://github.com/user-attachments/assets/79220db3-9920-47ea-a448-c66e1fbeb949)

```
update PRODUCTS

set reorder_lvl=reorder_lvl*0.7

where product_name like '%cream%'

and quantity>reorder_lvl;
```

**Output:**

![image](https://github.com/user-attachments/assets/c7794ce9-f291-4cb1-9fd4-ac0994d054f4)

**Question 2**

Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.

![image](https://github.com/user-attachments/assets/1aa6b872-0d06-4ce7-80e3-7c85154826c5)

```
update Suppliers

set address= '58 Lakeview, Magnolia'

where supplier_id=5;
```

**Output:**

![image](https://github.com/user-attachments/assets/b2e0e836-404c-41c7-ae6c-5724881b8911)

**Question 3**

Write a SQL statement to Increase the selling price by 15% in the products table where quantity in stock is less than 50 and supplier ID is 10.

![image](https://github.com/user-attachments/assets/c6367757-fd62-4bf9-9799-e4485927a7a8)

```
update Products

set sell_price=sell_price*1.15

where quantity<50

and supplier_id=10;
```

**Output:**

![image](https://github.com/user-attachments/assets/58b09089-1ea3-4814-9cb1-9a355a7666c9)

**Question 4**

For Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

![image](https://github.com/user-attachments/assets/ab5e782b-214e-4210-a344-80cba773ab9e)

```
update Products

set sell_price=sell_price*1.15

where quantity<50

and supplier_id=10;
```

**Output:**

![image](https://github.com/user-attachments/assets/c99ddf30-c492-4838-82c8-45d4456423f2)

**Question 5**

For Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

![image](https://github.com/user-attachments/assets/5fb594d8-e0cd-4af8-8f20-aa1a03569686)

```
update SALES

set sell_price=sell_price+3

where product_id in(select product_id

from PRODUCTS

where supplier_id=4 );
```

**Output:**

![image](https://github.com/user-attachments/assets/5a65b690-abc1-4f33-bbae-30075921eddd)

**Question 6**

Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'

![image](https://github.com/user-attachments/assets/63ee743e-6294-483c-ad4c-defb851b0d46)

```
UPDATE Employees

set salary=salary*2

where department_id=20

and job_id like '%MAN';
```

**Output:**

![image](https://github.com/user-attachments/assets/0728490e-6602-4c5a-8e24-e781d97a4e0e)

**Question 7**

Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

![image](https://github.com/user-attachments/assets/f02468d8-a468-46b4-b135-43cb93a1bbbe)

```
delete from Surgeries

where surgery_date='2024-02-28';
```

**Output:**

![image](https://github.com/user-attachments/assets/66acac18-605d-47e1-b847-cacb0124e82e)

**Question 8**

Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.

![image](https://github.com/user-attachments/assets/5a71a3e0-b295-4dcd-96d9-aec77149cc1f)

```
delete from Customer

where CUST_CITY!='New York'

and OUTSTANDING_AMT>5000;
```

**Output:**

![image](https://github.com/user-attachments/assets/4161feb8-01e9-408d-a961-45797a8b2cff)

**Question 9**

Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.

![image](https://github.com/user-attachments/assets/8b247064-2352-4fe7-acdd-1711eea27ed1)

```
delete from Doctors

where Specialization in ('Pediatrics','Cardiology')

and last_name like '%Brown%';
```

**Output:**

![image](https://github.com/user-attachments/assets/269b81dd-fa71-45a9-858f-55b5285ea606)

**Question 10**

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.

![image](https://github.com/user-attachments/assets/a25ffa8b-c335-44c1-82c3-9143c317ee2f)

```
delete from Customer

where GRADE>=2;
```

**Output:**

![image](https://github.com/user-attachments/assets/7c5acc0e-05ec-4da4-98a1-957cf3d953f8)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
