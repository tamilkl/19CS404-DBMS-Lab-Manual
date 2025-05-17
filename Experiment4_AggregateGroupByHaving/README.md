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

How many patients have expired insurance coverage for each insurance company?

Sample table:Insurance Table

![image](https://github.com/user-attachments/assets/24c11c16-fda1-48d6-8d6e-2e159a24cffc)

```
select InsuranceCompany,count(*) as TotalExpiredPatients

from Insurance

group by InsuranceCompany;

```

**Output:**

![image](https://github.com/user-attachments/assets/20e858b4-22b0-48c6-9bf3-9d2c7a4998dc)

**Question 2**

How many prescriptions were written by each doctor? Sample tablePrescriptions Table

![image](https://github.com/user-attachments/assets/2faf38d5-f5a1-4aaa-8f66-f90287a56872)

```
SELECT DoctorID,count(*) as TotalPrescriptions

from Prescriptions

group by DoctorID;
```

**Output:**

![image](https://github.com/user-attachments/assets/bf51c0bd-1599-496a-98b5-6f16c0d9fbf8)

**Question 3**

What is the total number of appointments scheduled by each doctor?

Sample table:Appointments Table

![image](https://github.com/user-attachments/assets/75c5ce93-a221-4c68-8a23-7161ed3a5e77)

**Output:**

![image](https://github.com/user-attachments/assets/4a9b35c7-4a2e-4300-b081-cad01604449f)

**Question 4**

Write a SQL query to find the Fruit with the lowest available quantity.

![image](https://github.com/user-attachments/assets/27cf1e74-1c19-4490-9ebe-23065a526b91)

```
select name as fruit_name , min(inventory) as lowest_quantity

from fruits;
```

**Output:**

![image](https://github.com/user-attachments/assets/bd2f72ed-db09-42cc-bd75-8c7878707651)

**Question 5**

Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count.

Note: Inventory attribute contains amount of fruits

![image](https://github.com/user-attachments/assets/2cb61809-cb7d-4351-ba8f-329cc294fb9e)

```
select sum(inventory) as total_available_amount

from fruits

where price>0.5;
```

**Output:**

![image](https://github.com/user-attachments/assets/213bbf0d-1557-4f0a-ab42-5e5a61952cc2)

**Question 6**

Write a SQL query to find the average salary of all employees?

![image](https://github.com/user-attachments/assets/1e77a350-4bbf-495d-a20b-e8ccc5e31c02)

```
select avg(income) as Average_Salary

from employee;
```

**Output:**

![image](https://github.com/user-attachments/assets/c8b2bf66-ee97-44ba-9bd0-20adb5da7362)

**Question 7**

Write a SQL query to determine the number of customers who received at least one grade for their activity.

![image](https://github.com/user-attachments/assets/70e5a71c-884e-44c8-8eb6-8ab639e59296)

```
SELECT COUNT(customer_id) AS COUNT

FROM customer

where grade is not null;
```

**Output:**

![image](https://github.com/user-attachments/assets/9fba989d-16ad-4a8f-a97f-49b6182e764f)

**Question 8**

Write the SQL query that accomplishes the selection of total cost of all products in each category from the "products" table and includes only those products where the total cost is greater than 50.

![image](https://github.com/user-attachments/assets/d680ceea-5815-4afe-9118-552602c81b16)

```
select category_id,sum(price) as Total_Cost

from products

group by category_id

having Total_Cost>50;

```

**Output:**

![image](https://github.com/user-attachments/assets/2326d0a2-ebca-40af-99dc-d723c10dd25d)

**Question 9**

Write a SQL query to find the difference between the maximum and minimum price of fruits?

![image](https://github.com/user-attachments/assets/e8e12762-d3dd-4176-bc4f-b59d792ddf06)

```
select (max(price)-min(price)) as price_diff

from fruits;
```

**Output:**

![image](https://github.com/user-attachments/assets/193b77e0-d6a4-4870-afad-756785be4d0e)

**Question 10**

Write a SQL query to find the average length of names for people living in Chennai?


![image](https://github.com/user-attachments/assets/947d305b-13d2-44b3-91d9-b48aa2c0bb8b)

```
select avg(length(name)) as avg_name_length

from customer

where city like '%Chennai%';

```

**Output:**

![image](https://github.com/user-attachments/assets/212949f5-a186-4f1e-9502-26bd35b00cd6)

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
