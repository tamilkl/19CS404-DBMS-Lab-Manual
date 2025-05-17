# Experiment 2: DDL Commands
## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**

Write a SQL query to Add a new column State as text in the Student_details table.

![image](https://github.com/user-attachments/assets/d77d70ca-7cc4-47a3-a7ce-561e45c87225)

```
ALTER TABLE Student_details ADD COLUMN State TEXT;
```
**Output:**

![image](https://github.com/user-attachments/assets/f6816446-02a5-413d-9601-895cd303be23)

**Question 2**

Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.
![image](https://github.com/user-attachments/assets/08bc811b-c5d7-41f6-b478-7141dd02a00c)

```
INSERT INTO Employee(EmployeeID,Name,Position)

VALUES('4','Emily White','Analyst');
```
**Output:**

![image](https://github.com/user-attachments/assets/16b0be4d-c367-4bc3-95b4-5b807c60220e)

**Question 3**

Insert all employees from Former_employees into Employee
![image](https://github.com/user-attachments/assets/e66a4127-0cce-4915-9bae-13a6d092006f)

```
INSERT into Employee(EmployeeID,Name,Department,Salary)

SELECT EmployeeID,Name,Department,Salary FROM Former_employees;
```

**Output:**

![image](https://github.com/user-attachments/assets/1f333654-e8c5-49a9-a068-6aba045e1102)

**Question 4**

Create a table named Customers with the following columns:

![image](https://github.com/user-attachments/assets/88d374de-5f2b-4682-90c4-8f19cf9053f5)

```
CREATE TABLE Customers(

CustomerID INTEGER,

Name TEXT,

Email TEXT,

JoinDate DATETIME );
```

**Output:**

![image](https://github.com/user-attachments/assets/c442f95f-4b2c-4db6-bda2-64ee8e1b39a3)

**Question 5**

Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

![image](https://github.com/user-attachments/assets/5c0fa14e-1bf8-43ff-afbd-e49c1ce47281)


```
ALTER TABLE Student_details

ADD COLUMN email TEXT not NULL default'Invalid';
```

**Output:**

![image](https://github.com/user-attachments/assets/3ebb9f54-625e-4b4f-82ce-43e18b3daf25)

**Question 6**

Create a table named Invoices with the following constraints:

InvoiceID as INTEGER should be the primary key.

InvoiceDate as DATE.

Amount as REAL should be greater than 0.

DueDate as DATE should be greater than the InvoiceDate.

OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

![image](https://github.com/user-attachments/assets/31231a61-66c7-4124-aa3a-3874e16cef1a)

```
CREATE TABLE Invoices(

InvoiceID INTEGER primary key,

InvoiceDate DATE,

Amount REAL CHECK(Amount>=0),

DueDate DATE CHECK(DueDate>=InvoiceDate),

OrderID INTEGER,

foreign key (OrderID) references Orders(OrderID) );
```

**Output:**

![image](https://github.com/user-attachments/assets/e0ab9583-0db2-4eca-9e63-dc63e08ef9bd)

**Question 7**

Create a table named Products with the following constraints:

ProductID should be the primary key.

ProductName should be NOT NULL.

Price is of real datatype and should be greater than 0.

Stock is of integer datatype and should be greater than or equal to 0.

![image](https://github.com/user-attachments/assets/be7c385b-05cb-448b-aeb4-fd356ab0bd89)


```
CREATE TABLE Products(

ProductID INTEGER primary key,

ProductName not NULL,

Price REAL CHECK (Price>0),

Stock INTEGER CHECK (Stock>=0) );
```

**Output:**

![image](https://github.com/user-attachments/assets/373a12e1-be4d-492e-bb30-934c7a5e621d)

**Question 8**

Create a table named Orders with the following constraints:

OrderID as INTEGER should be the primary key.

OrderDate as DATE should be not NULL.

CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

![image](https://github.com/user-attachments/assets/168ffca6-bc2f-4a19-aef6-9f2525c33d66)

```
CREATE TABLE Orders(

OrderID INTEGER primary key,

OrderDate DATE not NULL,

CustomerID INTEGER,

foreign key (CustomerID) references Customers(CustomerID) );
```

**Output:**

![image](https://github.com/user-attachments/assets/290298ca-0552-413d-973a-2e3e42526382)

**Question 9**

Create a table named Department with the following constraints:

DepartmentID as INTEGER should be the primary key.

DepartmentName as TEXT should be unique and not NULL.

Location as TEXT.

![image](https://github.com/user-attachments/assets/9eb859ca-e2ea-4aef-8194-fa05a7e7b81f)

```
CREATE TABLE Department(

DepartmentID INTEGER primary key,

DepartmentName TEXT UNIQUE not NULL,

Location TEXT );
```

**Output:**

![image](https://github.com/user-attachments/assets/a0f9475d-5f7a-42d1-9180-133f6798fe63)

**Question 10**

In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

![image](https://github.com/user-attachments/assets/c2e243e4-4987-46ea-b19f-eda6f1a84819)

```
INSERT INTO Books(ISBN, Title, Author, Publisher, Year)

VALUES('978-1234567890', 'Introduction to AI', 'John Doe', null, null);

INSERT INTO Books(ISBN, Title, Author, Publisher, Year)

VALUES('978-9876543210', 'Deep Learning', 'Jane Doe', 'TechPress', '2022');

INSERT INTO Books(ISBN, Title, Author, Publisher, Year)

VALUES('978-1122334455', 'Cybersecurity Essentials', 'Alice Smith', null, 2021);
```

**Output:**

![image](https://github.com/user-attachments/assets/53eeea10-ac1d-43c7-8ff6-18e45babb0ad)

## RESULT

Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
