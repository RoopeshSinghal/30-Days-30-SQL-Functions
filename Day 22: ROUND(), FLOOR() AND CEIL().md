## Day 22: ROUND(), FLOOR() AND CEIL()

The SQL `ROUND()`, `FLOOR()`, and `CEIL()` functions are used to manipulate numeric values in SQL. These functions are helpful in financial calculations, reporting, and scenarios requiring precise rounding or truncation of numbers.  

### Syntax:

-ROUND()
<br>Rounds a number to the nearest integer or to a specified decimal place

```sql
SELECT ROUND(number, decimals); 
```
 • Number: refers to the number you want to round.
 <br>• Decimals: specify the number of decimal places to round to.

-FLOOR() 
<br>Returns the largest integer less than or equal to the given number.

```sql
SELECT FLOOR(number); 
```

-CEIL()
<br>Returns the smallest integer greater than or equal to the given number.

```sql
SELECT CEIL(number); 
```

### Example:

The following demonstrates the usage of round, floor, and ceil functions for the calculation of tax and the subsequent determination of the total price, being the sum of the price and the computed tax.

Suppose the price of a product is $99.99, and the tax rate is 5%. Calculate the tax amount and the total price using each function.  

```sql
SELECT 'rounded_tax' AS Metric, ROUND(99.99 * 0.05, 2) AS Value
UNION ALL
SELECT 'floored_tax', FLOOR(99.99 * 0.05)
UNION ALL
SELECT 'ceiled_tax', CEIL(99.99 * 0.05)
UNION ALL
SELECT 'rounded_total_price', ROUND(99.99 + ROUND(99.99 * 0.05, 2), 2)
UNION ALL
SELECT 'floored_total_price', FLOOR(99.99 + FLOOR(99.99 * 0.05))
UNION ALL
SELECT 'ceiled_total_price', CEIL(99.99 + CEIL(99.99 * 0.05));
```

Output:  
| Metric                 | Value   |
|------------------------|---------|
| rounded_tax            | 5.00    |
| floored_tax            | 4       |
| ceiled_tax             | 5       |
| rounded_total_price    | 104.99  |
| floored_total_price    | 103     |
| ceiled_total_price     | 105     |

### Question:

### Problem Statement

You are managing an employee payroll system. The salary details are stored in the `employee_salaries` table, which has the following schema:

Schema:
| Column Name      | Data Type  | Description                            |  
|------------------|------------|----------------------------------------|  
| employee_id      | INT        | Unique ID for each employee            |  
| employee_name    | VARCHAR(50)| Name of the employee                   |  
| base_salary      | DECIMAL(10,2) | Monthly base salary of the employee |  
| tax_rate         | DECIMAL(5,2) | Tax rate percentage applicable         |  

Task:

1. Calculate Tax Amount: Determine the tax amount for each employee by multiplying their `base_salary` by the `tax_rate`.
2. Calculate Net Salary: 
    - Calculate the `net_salary` for each employee by subtracting the `tax_amount` from their `base_salary`.
    - Calculate three variations of net salary:
        • `rounded_net_salary`: Round the `net_salary` to two decimal places.
        • `floored_net_salary`: Truncate the `net_salary` to the nearest integer (downwards).
        • `ceiled_net_salary`: Round the `net_salary` to the nearest integer (upwards).
3. Display Results:
    - Create a result table with the following columns:
        • `employee_id`
        • `employee_name`
        • `tax_amount`
        • `rounded_net_salary`
        • `floored_net_salary`
        • `ceiled_net_salary`

### Schema setup

```sql
CREATE TABLE employee_salaries (
    employee_id INT,
    employee_name VARCHAR(50),
    base_salary DECIMAL(10,2),
    tax_rate DECIMAL(5,2)
);

INSERT INTO employee_salaries (employee_id, employee_name, base_salary, tax_rate) VALUES
(1, 'Alice Johnson', 5000.00, 10.00),
(2, 'Bob Smith', 7500.50, 15.00),
(3, 'Charlie Brown', 10000.00, 20.00),
(4, 'Diana Prince', 12000.75, 12.50),
(5, 'Evan Lee', 6500.30, 8.00),
(6, 'Fiona White', 4200.00, 18.00),
(7, 'George Black', 9700.25, 22.00),
(8, 'Hannah Adams', 8400.60, 9.00),
(9, 'Ian Gray', 5600.80, 5.50),
(10, 'Jack Green', 6800.90, 11.00);
```

### Expected output

Expected Output:
| employee_id | employee_name  | tax_amount | rounded_net_salary | floored_net_salary | ceiled_net_salary |  
|-------------|----------------|------------|--------------------|--------------------|-------------------|  
| 1           | Alice Johnson  | 500.00     | 4500.00            | 4500               | 4500              |  
| 2           | Bob Smith      | 1125.08    | 6375.42            | 6375               | 6376              |  
| 3           | Charlie Brown  | 2000.00    | 8000.00            | 8000               | 8000              |  
| 4           | Diana Prince   | 1500.09    | 10500.66           | 10500              | 10501             |  
| 5           | Evan Lee       | 520.02     | 5979.28            | 5979               | 5980              |  
| 6           | Fiona White    | 756.00     | 3444.00            | 3444               | 3445              |  
| 7           | George Black   | 2134.06    | 7566.19            | 7566               | 7567              |  
| 8           | Hannah Adams   | 756.05     | 7644.55            | 7644               | 7645              |  
| 9           | Ian Gray       | 308.04     | 5292.76            | 5292               | 5293              |  
| 10          | Jack Green     | 748.10     | 6052.80            | 6052               | 6053              |    

### Solution Query

```sql
Will Be Added Tomorrow
```
