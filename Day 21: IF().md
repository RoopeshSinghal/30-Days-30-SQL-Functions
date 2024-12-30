## Day 21: IF()

The SQL `IF()` function works like a conditional statement in Excel, allowing you to evaluate a condition and return different results based on whether the condition is true or false.

### Syntax:

```sql
SELECT IF(condition, value_if_true, value_if_false);
```

 • condition – It is used to specify the condition to be evaluated.
 <br>• value_if_true – It is an optional parameter that is used to specify the value to be returned if the condition evaluates to be true.
 <br>• value_if_false – It is an optional parameter that is used to specify the value to be returned if the condition evaluates to be false.

### Example:

The following example demonstrates the application of an if function for assessing sales status, namely, to ascertain if total sales exceed the predetermined target

Suppose you want to check whether a sales figure exceeds a target of 5000

```sql
SELECT
     sales_id,  
     total_sales,  
     IF(total_sales > 5000, 'Above Target', 'Below Target') AS sales_status  
FROM sales;  
```

Output:  
| sales_id | total_sales | sales_status   |  
|----------|-------------|----------------|  
| 1        | 6200        | Above Target   |  
| 2        | 4300        | Below Target   |  
| 3        | 5100        | Above Target   |  

### Question:

### Problem Statement

You are managing an employee database for a company that provides bonuses to employees who have worked a certain number of hours during the month of December.

Schema:
| Column Name   | Data Type    | Description                                |  
|---------------|--------------|--------------------------------------------|  
| employee_id   | INT          | Unique ID for each employee                |  
| employee_name | VARCHAR(50)  | Name of the employee                       |  
| base_salary   | DECIMAL(10,2)| Monthly base salary of the employee        |  
| hours_worked  | INT          | Total hours worked in December             |  

The bonus calculation depends on the number of hours worked:  

1. If the employee has worked more than 160 hours, they receive a 20% bonus of their base salary.  
2. If the employee has worked between 120 and 160 hours, they receive a 10% bonus of their base salary.  
3. If the employee has worked less than 120 hours, they receive no bonus.  

Task
Write a query to calculate and display:  
1. `employee_id`: The unique ID of the employee.  
2. `hours_worked`: The total hours worked by the employee in December.  
3. `base_salary`: The base salary of the employee.  
4. `bonus`: The bonus amount calculated using the above rules.  
5. `total_salary`: The sum of the base salary and the bonus.
   
### Schema setup

```sql
CREATE TABLE employees (  
    employee_id INT,  
    employee_name VARCHAR(50),  
    base_salary DECIMAL(10,2),  
    hours_worked INT  
);  

INSERT INTO employees (employee_id, employee_name, base_salary, hours_worked) VALUES  
(1, 'Alice Johnson', 3000.00, 170),  
(2, 'Bob Smith', 2500.00, 145),  
(3, 'Carol Lee', 4000.00, 110),  
(4, 'David Brown', 3500.00, 180),  
(5, 'Emma Davis', 2800.00, 95),  
(6, 'Frank White', 3200.00, 160);  
```

### Expected output

| employee_id | employee_name  | hours_worked | base_salary | bonus    | total_salary |  
|-------------|----------------|--------------|-------------|----------|--------------|  
| 4           | David Brown    | 180          | 3500.00     | 700.00   | 4200.00      |  
| 1           | Alice Johnson  | 170          | 3000.00     | 600.00   | 3600.00      |  
| 6           | Frank White    | 160          | 3200.00     | 320.00   | 3520.00      |  
| 2           | Bob Smith      | 145          | 2500.00     | 250.00   | 2750.00      |  
| 3           | Carol Lee      | 110          | 4000.00     | 0.00     | 4000.00      |  
| 5           | Emma Davis     | 95           | 2800.00     | 0.00     | 2800.00      |  

### Solution Query

```sql
SELECT  
    employee_id,  
    employee_name,  
    hours_worked,  
    base_salary,  
    IF(hours_worked > 160, base_salary * 0.2,   
       IF(hours_worked BETWEEN 120 AND 160, base_salary * 0.1, 0)) AS bonus,  
    base_salary +  
    IF(hours_worked > 160, base_salary * 0.2,   
       IF(hours_worked BETWEEN 120 AND 160, base_salary * 0.1, 0)) AS total_salary  
FROM employees  
ORDER BY total_salary DESC;
```
