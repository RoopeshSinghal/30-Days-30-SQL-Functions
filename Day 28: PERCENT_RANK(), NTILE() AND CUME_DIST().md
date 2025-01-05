## Day 28: PERCENT_RANK(), NTILE() AND CUME_DIST()

These advanced window functions in SQL provide insights into the relative position and distribution of rows within a partition. They are particularly useful for percentiles, ranking, and data segmentation.

1. PERCENT_RANK(): Calculates the relative rank of a row as a percentage of the total number of rows in the partition.

2. NTILE(): Divides the dataset into a specified number of equal-sized groups and assigns a group number to each row.  

3. CUME_DIST(): Calculates the cumulative distribution of a row, showing the proportion of rows with values less than or equal to the current row.

### Syntax:

```sql
SELECT PERCENT_RANK() / NTILE(n) / CUME_DIST()  OVER (PARTITION BY column_name ORDER BY column_name)
FROM tablename
```

### Example:

This example demonstrates how these functions work to provide insights into data distribution and ranking.  

Imagine a table named `Sales` with the following columns:  

• `salesperson_id`: Unique identifier for each salesperson  
• `region`: Sales region  
• `sales_amount`: Total sales amount  

Input:  
| salesperson_id | region | sales_amount |
|----------------|--------|--------------|
| 1              | North  | 10000        |
| 2              | North  | 15000        |
| 3              | North  | 20000        |
| 4              | South  | 25000        |
| 5              | South  | 30000        |
| 6              | South  | 30000        | 

```sql
SELECT  
  salesperson_id,  
  region,  
  sales_amount,  
  PERCENT_RANK() OVER (PARTITION BY region ORDER BY sales_amount) AS percent_rank,  
  NTILE(3) OVER (PARTITION BY region ORDER BY sales_amount) AS ntile_group,  
  CUME_DIST() OVER (PARTITION BY region ORDER BY sales_amount) AS cume_dist  
FROM  
  Sales;  
```

Output:
| salesperson_id | region | sales_amount | percent_rank | ntile_group | cume_dist |
|----------------|--------|--------------|--------------|-------------|-----------|
| 1              | North  | 10000        | 0.0000       | 1           | 0.3333    |
| 2              | North  | 15000        | 0.5000       | 2           | 0.6667    |
| 3              | North  | 20000        | 1.0000       | 3           | 1.0000    |
| 4              | South  | 25000        | 0.0000       | 1           | 0.3333    |
| 5              | South  | 30000        | 0.5000       | 2           | 1.0000    |
| 6              | South  | 30000        | 0.5000       | 3           | 1.0000    |

Explanation:

1. PERCENT_RANK():  
   - Calculates the relative rank of each row within its partition.  
   - In the South region, the first row (sales_amount: 25000) gets a percent rank of 0.0000. The two tied rows (sales_amount: 30000) share the same rank of 0.5000.  

2. NTILE():  
   - Divides the rows into three groups (as specified by `NTILE(3)`) within each region.  
   - For example, in the South region, the first row (25000) falls into group 1, while the tied rows (30000) are split into groups 2 and 3.  

3. CUME_DIST():  
   - Shows the proportion of rows with values less than or equal to the current row.  
   - In the South region, the tied rows (30000) both have a cumulative distribution of 1.0000 since they represent the last rows in the partition.
   
### Question:

### Problem Statement

You are a data analyst at an e-commerce company. Your task is to analyze the distribution of product sales across different regions.
Each sale has a unique `sale_id`, and the dataset includes the region where the sale occurred and the total sales amount.  

Schema:
Table Name:`Sales`  
| Column Name  | Data Type   | Description                     |  
|--------------|-------------|---------------------------------|  
| sale_id      | INT         | Unique identifier for each sale |  
| region       | VARCHAR(10) | Region where the sale occurred  |  
| sales_amount | INT         | Total sales amount for the sale |  

Task: 

The company wants you to write a query to:  
1. Divide the sales into quartiles.
2. Calculate the relative rank of each sale in its region. 
3. Calculate the cumulative distribution of each sale.  
4. Display the following columns in the result:  
   - `region`  
   - `sale_id`  
   - `sales_amount`  
   - `relative_rank`  
   - `quartile`  
   - `cum_dist`  

### Schema setup

```sql
CREATE TABLE Sales (  
    sale_id INT PRIMARY KEY,  
    region VARCHAR(10),  
    sales_amount INT 
);  

INSERT INTO Sales (sale_id, region, sales_amount) VALUES  
(1, 'North', 5000.00),  
(2, 'North', 7000.00),  
(3, 'North', 8000.00),  
(4, 'North', 10000.00),  
(5, 'South', 6000.00),  
(6, 'South', 9000.00),  
(7, 'South', 10000.00),  
(8, 'South', 12000.00),  
(9, 'East', 4000.00),  
(10, 'East', 4000.00),  
(11, 'East', 6000.00),  
(12, 'East', 7000.00);  
```

### Expected output

| sale_id | region | sales_amount | quartile | relative_rank | cum_dist |
|---------|--------|--------------|----------|---------------|----------|
| 1       | North  | 5000         | 1        | 0             | 0.25     |
| 2       | North  | 7000         | 2        | 0.33          | 0.5      |
| 3       | North  | 8000         | 3        | 0.67          | 0.75     |
| 4       | North  | 10000        | 4        | 1             | 1        |
| 5       | South  | 6000         | 1        | 0             | 0.25     |
| 6       | South  | 9000         | 2        | 0.33          | 0.5      |
| 7       | South  | 10000        | 3        | 0.67          | 0.75     |
| 8       | South  | 12000        | 4        | 1             | 1        |
| 9       | East   | 4000         | 1        | 0             | 0.5      |
| 10      | East   | 4000         | 2        | 0             | 0.5      |
| 11      | East   | 6000         | 3        | 0.67          | 0.75     |
| 12      | East   | 7000         | 4        | 1             | 1        |

### Solution Query

```sql
Will Be Added Tommorrow
```
