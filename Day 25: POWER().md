## Day 25: POWER()

The SQL POWER() function raises a number to the power of another number. It is used to calculate exponential values in SQL queries.

### Syntax:

```sql
SELECT POWER(base, exponent);  
```

• base: The numeric value that will be raised to the power of the exponent.
<br>• exponent: The numeric value representing the power to which the base will be raised.  

### Example:

The following example demonstrates the use of the SQL POWER function to calculate the compound interest:

Suppose we want to calculate the compound interest for a set of accounts with different interest rates. We have a table named "accounts" with columns "account_id" and "interest_rate." We want to raise each interest rate to the power of 2 to calculate the compound interest factor.

```sql
SELECT
    account_id,
    POWER(interest_rate, 2) AS compound_interest_factor
FROM accounts;
```

Input:
| account_id | interest_rate |
|------------|---------------|
| 1          | 0.03          |
| 2          | 0.05          |
| 3          | 0.04          |
| 4          | 0.06          |

Output:
| account_id | compound_interest_factor |
|------------|--------------------------|
| 1          | 0.0009                   |
| 2          | 0.0025                   |
| 3          | 0.0016                   |
| 4          | 0.0036                   |

This result shows the compound interest factors for each account, which are calculated by raising the interest rates to the power of 2.

### Question:

### Problem Statement

You are a data analyst working for a retail company. The company tracks product sales across different regions and wants to predict future revenue growth. The sales data is stored in the `sales_data` table.  

Calculate the projected revenue for each product after applying a growth rate for the next 3 years.  

Schema:  
Table Name: `sales_data`  
| Column Name       | Data Type   | Description                           |  
|-------------------|-------------|---------------------------------------|  
| product_id        | INT         | Unique identifier for each product    |  
| product_name      | VARCHAR(50) | Name of the product                   |  
| current_revenue   | INT         | Revenue generated in the current year |  
| annual_growth_rate| FLOAT       | Annual growth rate                    |  

Task:  

1. Calculate the projected revenue for each product after 3 years using the formula:  
   Projected Revenue = current_revenue * (1 + annual_growth_rate)^3

2. Display the following columns:  
   - `product_id`  
   - `product_name`  
   - `current_revenue`  
   - `annual_growth_rate`  
   - `projected_revenue`  
   
### Schema setup

```sql
CREATE TABLE sales_data (  
    product_id INT,  
    product_name VARCHAR(50),  
    current_revenue INT,  
    annual_growth_rate FLOAT  
);  

INSERT INTO sales_data (product_id, product_name, current_revenue, annual_growth_rate) VALUES  
(1, 'Laptop', 50000, 0.10),  
(2, 'Smartphone', 30000, 0.08),  
(3, 'Tablet', 20000, 0.05),  
(4, 'Smartwatch', 15000, 0.07),  
(5, 'Desktop', 40000, 0.09);  
```

### Expected output

| product_id | product_name | current_revenue | annual_growth_rate  | projected_revenue |
|------------|--------------|-----------------|---------------------|-------------------|
| 1          | Laptop       | 50000           | 0.1                 | 66550             |
| 2          | Smartphone   | 30000           | 0.08                | 37791             |
| 3          | Tablet       | 20000           | 0.05                | 23153             |
| 4          | Smartwatch   | 15000           | 0.07                | 18376             |
| 5          | Desktop      | 40000           | 0.09                | 51801             | 

### Solution Query

```sql
Will Be Added Tomorrow
```
