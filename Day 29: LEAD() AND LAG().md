## Day 29: LEAD() AND LAG()  

The `LEAD()` and `LAG()` functions in SQL are used for accessing data from subsequent or preceding rows in the same result set without the use of self-joins. They are essential in performing calculations or comparisons between rows, especially in time-series or sequential data analysis.  

1. LEAD(): Fetches data from the next row within the same result set.
   
2. LAG(): Fetches data from the previous row within the same result set

### Syntax:

```sql
SELECT
  LEAD / LAG(column_name, offset, default_value) OVER (PARTITION BY column_name ORDER BY column_name)
FROM tablename;
```

### Example:

The following example demonstrates the working of lead and lag function.

Imagine a table Employee_Salary that records salary changes for employees over time.  
Input:
| employee_id | salary_date | salary |  
|-------------|-------------|--------|  
| 1           | 2023-01-01  | 50000  |  
| 1           | 2023-07-01  | 55000  |  
| 1           | 2024-01-01  | 60000  |  
| 2           | 2023-03-01  | 45000  |  
| 2           | 2023-09-01  | 47000  |  
| 2           | 2024-03-01  | 49000  |  

The following query compares the current salary with the previous and next salaries for each employee:  

```sql
SELECT  
    employee_id,  
    salary_date,  
    salary,  
    LAG(salary) OVER (PARTITION BY employee_id ORDER BY salary_date) AS previous_salary,  
    LEAD(salary) OVER (PARTITION BY employee_id ORDER BY salary_date) AS next_salary  
FROM  
    Employee_Salary;  
```

Output: 
| employee_id | salary_date | salary | previous_salary | next_salary |  
|-------------|-------------|--------|-----------------|-------------|  
| 1           | 2023-01-01  | 50000  | NULL            | 55000       |  
| 1           | 2023-07-01  | 55000  | 50000           | 60000       |  
| 1           | 2024-01-01  | 60000  | 55000           | NULL        |  
| 2           | 2023-03-01  | 45000  | NULL            | 47000       |  
| 2           | 2023-09-01  | 47000  | 45000           | 49000       |  
| 2           | 2024-03-01  | 49000  | 47000           | NULL        |  
   
### Question:

### Problem Statement

Analyze Percentage Change in Game Sales on the Steam Store  

As a data analyst for a gaming company, your task is to analyze the sales trends for selected games on the Steam store.
Using sales data for four popular games — Valorant, Marvel Rivals, COD (Call of Duty), and PUBG PC, calculate the percentage change in monthly sales.  

Schema:
Table Name: Game_Sales
| Column Name      | Data Type   | Description                                    |  
|------------------|-------------|------------------------------------------------|  
| game_name        | VARCHAR(20) | Name of the game                               |  
| sales_month      | DATE        | Month of the sales record                      |  
| sales_units      | INT         | Total number of units sold in the given month  |  

Task: 

1. Use the appropriate function to fetch the previous month's sales for each game.  
2. Calculate the percentage change in sales between the current and previous month.  
3. Display the following columns:  
   - `game_name`  
   - `sales_month`  
   - `sales_units`  
   - `previous_sales` 
   - `percentage_change`
4. Handle scenarios where there is no previous month's data by displaying `NULL` for the percentage change.

### Schema setup

```sql
CREATE TABLE Game_Sales (  
 game_name VARCHAR(20),  
 sales_month DATE,  
 sales_units INT  
);  

INSERT INTO Game_Sales (game_name, sales_month, sales_units) VALUES  
('Valorant', '2024-10-01', 120000),  
('Valorant', '2024-11-01', 135000),  
('Valorant', '2024-12-01', 145000),  
('Marvel Rivals', '2024-10-01', 80000),  
('Marvel Rivals', '2024-11-01', 95000),  
('Marvel Rivals', '2024-12-01', 97000),  
('COD', '2024-10-01', 100000),  
('COD', '2024-11-01', 120000),  
('COD', '2024-12-01', 110000),  
('PUBG PC', '2024-10-01', 150000),  
('PUBG PC', '2024-11-01', 140000),  
('PUBG PC', '2024-12-01', 160000);  
```

### Expected output

| game_name      | sales_month | sales_units | previous_sales | percentage_change |  
|----------------|-------------|-------------|----------------|-------------------|  
| Valorant       | 2024-10-01  | 120000      | NULL           | NULL              |  
| Valorant       | 2024-11-01  | 135000      | 120000         | 12.50             |  
| Valorant       | 2024-12-01  | 145000      | 135000         | 7.41              |  
| Marvel Rivals  | 2024-10-01  | 80000       | NULL           | NULL              |  
| Marvel Rivals  | 2024-11-01  | 95000       | 80000          | 18.75             |  
| Marvel Rivals  | 2024-12-01  | 97000       | 95000          | 2.11              |  
| COD            | 2024-10-01  | 100000      | NULL           | NULL              |  
| COD            | 2024-11-01  | 120000      | 100000         | 20.00             |  
| COD            | 2024-12-01  | 110000      | 120000         | -8.33             |  
| PUBG PC        | 2024-10-01  | 150000      | NULL           | NULL              |  
| PUBG PC        | 2024-11-01  | 140000      | 150000         | -6.67             |  
| PUBG PC        | 2024-12-01  | 160000      | 140000         | 14.29             |  
### Solution Query

```sql
Will Be Added Tomorrow
```
