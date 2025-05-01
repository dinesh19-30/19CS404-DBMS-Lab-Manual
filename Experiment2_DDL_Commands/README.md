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
---
Create a table named Events with the following columns:

EventID as INTEGER
EventName as TEXT
EventDate as DATE

```sql
CREATE TABLE Events(
EventID INTEGER,
EventName TEXT,
EventDate  DATE);
```

**Output:**
![out1](https://github.com/user-attachments/assets/041c5bb4-ef81-4456-888c-b505282adb55)


**Question 2**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

```sql
ALTER TABLE employee
ADD COLUMN department_id INTEGER;
ALTER TABLE employee
ADD COLUMN manager_id INTEGER DEFAULT NULL;
```

**Output:**

![Output2]![image](https://github.com/user-attachments/assets/f4a93e0e-4864-48fe-a360-69885eedb584)


**Question 3**
---
Insert the below data into the Employee table, allowing the Department and Salary columns to take their default values.

EmployeeID  Name         Position
----------  -----------  ----------
4           Emily White  Analyst

Note: The Department and Salary columns will use their default values. 

```sql
INSERT INTO Employee(EmployeeID,Name,Position)
VALUES(4,"Emily White","Analyst");
```

**Output:**

![Output3]![image](https://github.com/user-attachments/assets/fbbacbfb-70cc-477b-9a6d-47ab739734ab)


**Question 4**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables
107         Laptop            Electronics  999.99      50
108         Wireless Earbuds  Accessories              100

```sql
INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(106,'Fitness Tracker','Wearables',NULL,NULL);

INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(107,'Laptop','Electronic',999.99,50);

INSERT INTO Products(ProductID,Name,Category,Price,Stock)
VALUES(108,'Wireless Earbud','Accessorie',NULL,100);
```

**Output:**

![Output4]![image](https://github.com/user-attachments/assets/022310ba-ce57-4097-aa99-4213d78f988c)


**Question 5**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql
create table Employees(
EmployeeID INTEGER PRIMARY KEY,
FirstName TEXT NOT NULL,
LastName TEXT NOT NULL,
Email TEXT UNIQUE,
Salary DECIMAL(10,2) CHECK(Salary > 0),
DepartmentID INTEGER,
FOREIGN KEY(DepartmentID)REFERENCES Departments(DepartmentID)
)
```

**Output:**

![Output5]![image](https://github.com/user-attachments/assets/4d168c6a-bcbd-4f73-88b5-9ec399dfdd0f)


**Question 6**
---
Insert all books from Out_of_print_books into Books

Table attributes are ISBN, Title, Author, Publisher, YearPublished

```sql
INSERT INTO Books(ISBN, Title, Author, Publisher, YearPublished)
SELECT ISBN, Title, Author, Publisher, YearPublished
FROM Out_of_print_books;
```

**Output:**

![Output6]![image](https://github.com/user-attachments/assets/45d2ba45-4e60-496e-b8ff-9b58d049eeec)


**Question 7**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.

```sql
CREATE TABLE Department(
DepartmentID INTEGER PRIMARY KEY,
DepartmentName TEXT NOT NULL UNIQUE,
Location TEXT
);
```

**Output:**

![Output7]![image](https://github.com/user-attachments/assets/8f09760b-226c-4881-a665-591d55df0f2c)


**Question 8**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```sql
CREATE TABLE Orders(
OrderID integer primary key,
OrderDate date not null,
CustomerID integer,
foreign key (CustomerID) REFERENCES Customers(CustomerID)
);
```

**Output:**

![Output8]![image](https://github.com/user-attachments/assets/cec77c61-01d7-4039-8c9f-837f12fbb7df)


**Question 9**
---
Write an SQL query to add a new column salary of type INTEGER to the Employees table, with a CHECK constraint that ensures the value in this column is greater than 0.

```sql
ALTER TABLE Employees
ADD COLUMN(salary INTEGER);
```

**Output:**

![Output9]![image](https://github.com/user-attachments/assets/4fdedde8-f2ed-44fc-80a1-e857a62db7d7)


**Question 10**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price should be greater than 0.
Stock should be greater than or equal to 0.

```sql
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price should be greater than 0.
Stock should be greater than or equal to 0.
```

**Output:**

![Output10]  ![image](https://github.com/user-attachments/assets/0953b52e-bd49-4991-ae10-ef045d7e9f64)



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
