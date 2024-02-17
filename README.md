# SQL-Books-Startup

## Scenario 
The ficitonal bookstore has two SQL tables: `authors` and `books`.
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

The bookstore also has `event_log` that records every time an admin inserted an image into a book catalog. It has over 100k rows. The `event_date_time` might not look familiar for general audiences, however, it is similar to `epoch timestamp`. 

* Table `event_log`:
  
| employee_id | event_date_time |
|---|---|
| 7494212 | 1535308430 |
| 7494212 | 1535308433 |
| 1475185 | 1535308444 |
| 6946725 | 1535308475 |
| 6946725 | 1535308476 |
| 6946725 | 1535308477 |
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
2. Write an SQL query to find out how many users inserted more than 500 but less than 1000 images in their presentations!
3. Print every department where the average salary per employee is lower than $800!

## 
