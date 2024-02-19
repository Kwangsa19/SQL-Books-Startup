# SQL-Books-Startup
> This is a modified version of case study. Please visit this [link](https://data36.com/sql-interview-questions-tech-screening-data-analysts/). 

## Scenario 
The fictional bookstore has two SQL tables: `authors` and `books`.
The authors dataset has 1M+ rows. Here’s a small sample, the first six rows:

* Table `authors`:
  
| author_name | book_name |
|---|---|
| author_1 | book_1 |
| author_1 | book_2 |
| author_2 | book_3 |
| author_2 | book_4 |
| author_2 | book_5 |
| author_3 | book_6 |
| ..... | .....|

* Table `books`:
  
| book_name | sold_copies |
|---|---|
| book_1 | 1000 |
| book_2 | 1500 |
| book_3 | 34000 |
| book_4 | 29000 |
| book_5 | 40000 |
| book_6 | 4400 |
| ..... | .....|

The bookstore also has `employees` and `salaries` tables. The `employees` contains the employee names, the unique employees ids, and the department names of a company.

* Table `employees`:

| department_name | employee_id | employee_name |
|---|---|---|
| Sales | 7494212 | John Doe |
| Sales | 7494212 | Jane Smith |
| HR | 1475185 | Billy Bob |
| Sales | 6946725 | Robert Hayek |
| Marketing | 6946725 | Edward Jorgson |
| Marketing | 6946725 | Christine Packard |
| ..... | .....| ..... |

* Table `salaries`: 

| salary | employee_id | employee_name |
|---|---|---|
| 1000 | 7494212 | John Doe |
| 600 | 7494212 | Jane Smith |
| 1000 | 1475185 | Billy Bob |
| 400 | 6946725 | Robert Hayek |
| 1200 | 6946725 | Edward Jorgson |
| 200 | 6946725 | Christine Packard |
| ..... | .....| ..... |


Tasks: 
1. Create an SQL query that shows the TOP 3 authors who sold the most books in total!
2. Print every department where the average salary per employee is lower than $800!

## Database and Table
> Copy and paste this code into your SQL editor.

> This is conducted on MySQL/MariaDB relational database management system.

* Table `authors` and `books`
```
CREATE DATABASE books;

-- Create Authors table
CREATE TABLE authors (
    author_name VARCHAR(255),
    book_name VARCHAR(255)
);

-- Insert data into Authors
INSERT INTO authors (author_name, book_name) VALUES
('author_1', 'book_1'),
('author_1', 'book_2'),
('author_2', 'book_3'),
('author_2', 'book_4'),
('author_2', 'book_5'),
('author_3', 'book_6');

-- Create Books table
CREATE TABLE books (
    book_name VARCHAR(255),
    sold_copies INT
);

-- Insert data into Books
INSERT INTO books (book_name, sold_copies) VALUES
('book_1', 1000),
('book_2', 1500),
('book_3', 34000),
('book_4', 29000),
('book_5', 40000),
('book_6', 4400);

-- Create Employees table
CREATE TABLE employees (
    department_name VARCHAR(255),
    employee_id INT,
    employee_name VARCHAR(255)
);

-- Insert data into Employees
INSERT INTO employees (department_name, employee_id, employee_name) VALUES
('Sales', 123, 'John Doe'),
('Sales', 211, 'Jane Smith'),
('HR', 556, 'Billy Bob'),
('Sales', 711, 'Robert Hayek'),
('Marketing', 235, 'Edward Jorgson'),
('Marketing', 236, 'Christine Packard');

-- Create Salaries table
CREATE TABLE salaries (
    salary INT,
    employee_id INT,
    employee_name VARCHAR(255)
);

-- Insert data into Salaries
INSERT INTO salaries (salary, employee_id, employee_name) VALUES
(500, 123, 'John Doe'),
(600, 211, 'Jane Smith'),
(1000, 556, 'Billy Bob'),
(400, 711, 'Robert Hayek'),
(1200, 235, 'Edward Jorgson'),
(200, 236, 'Christine Packard');

```

## Solution
1. Create an SQL query that shows the TOP 3 authors who sold the most books in total:
   
```
SELECT authors.author_name, SUM(books.sold_copies) AS TotalSold
FROM authors
JOIN books -- Inner Join is also okay
ON authors.book_name = books.book_name
GROUP BY authors.author_name
ORDER BY TotalSold DESC
LIMIT 3; -- Just three
```
This query will show the top 3 authors who have sold the most books. 
* First, I selected the name of the authors from `authors.author_name` and `TotalSold`.
* Second, I combined two tables using `Join` or `Inner Join` on one condition the book name from `authors` table must match the name of the book in the `books` table.
* Third, I grouped them by their author names.
* Fourth, I reversed them on the `TotalSold` column.
* The output:

![heidisql_tUopEqH3BD](https://github.com/Kwangsa19/SQL-Books-Startup/assets/135963482/7fac874a-ec38-4e9e-a895-df56f494b68d)

2. Print every department where the average salary per employee is lower than $800: 

```
SELECT employees.department_name, AVG(salaries.salary) AS AverageSalary
FROM employees 
INNER JOIN salaries 
ON employees.employee_id = salaries.employee_id
GROUP BY department_name
HAVING AverageSalary < 800
ORDER BY AverageSalary DESC;
```
This query will print every department where the average salary per employee is lower than $800.
* First, I selected `department_name` from `employees` table and `AverageSalary`. These two will appear in the output. 
* Second, I inner joined both `employees` and `salaries` tables on one condition that `employees.employee.id` must match `salaries_employee_id`.
* Third, I grouped them based on the `department_name`. Initially, it would appear alphabetically and appear as they are. Remember, if you set the average salary under 800 first, then there would be an error due to MySQL selecting those deparment with below 800 in salary. Make sure it is on the fourth stage. 
* Fourth, I set one condition that the average salary has to be under 800. This will eliminate the error in the MySQL. 
* Fifth, I sorted the `AverageSalary` reversely.
* The output:

![heidisql_1rtzqMXGyV](https://github.com/Kwangsa19/SQL-Books-Startup/assets/135963482/7e2f01ae-4127-4782-b770-190a3d7b1b32)

## Conclusion
1. The top 3 authors are `author 2`, `author 3`, and `author 1`.
2. The departments where the average salary per employee are lower than $800 are : `Marketing` and `Sales`. 
