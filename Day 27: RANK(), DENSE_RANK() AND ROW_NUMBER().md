## Day 27: RANK(), DENSE_RANK() AND ROW_NUMBER()

Ranking functions in SQL are essential for assigning a unique rank or order to rows based on specific criteria. These functions are used to rank rows within a partition of a dataset.

1. RANK() 
 Assigns a rank to each row within a partition of a dataset. Duplicate values receive the same rank, but gaps appear in the sequence. 

2. DENSE_RANK() 
Similar to `RANK()`, but without gaps in the ranking sequence. Duplicate values receive the same rank and no gaps appear. 

3. ROW_NUMBER() 
Assigns a unique sequential number to each row.

### Syntax:

```sql
SELECT RANK() / DENSE_RANK() / ROW_NUMBER() OVER (PARTITION BY column_name ORDER BY column_name)
FROM tablename
```

### Example:

This example demonstrates how these three ranking functions can be used to rank data within a specific partition.

Imagine a table named `Employee` with the following columns:

• employee_id: Unique identifier for each employee
• department: Department the employee belongs to
• salary: Annual salary of the employee

We want to rank employees within each department based on their salary, using the three ranking functions: `RANK`, `DENSE_RANK`, and `ROW_NUMBER`.

Input:
| employee_id | department | salary |
|-------------|------------|--------|
| 1           | IT         | 50000  |
| 2           | IT         | 60000  |
| 3           | IT         | 60000  |
| 4           | HR         | 45000  |
| 5           | HR         | 55000  |
| 6           | Sales      | 70000  |
| 7           | Sales      | 65000  |
| 8           | Sales      | 65000  |

SELECT
 employee_id,
 department,
 salary,
 RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS rank,
 DENSE_RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS dense_rank,
 ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_number
FROM
 Employee;

Output:
| employee_id | department | salary | rank | dense_rank | row_number |
|-------------|------------|--------|------|------------|------------|
| 6           | Sales      | 70000  | 1    | 1          | 1          |
| 7           | Sales      | 65000  | 2    | 2          | 2          |
| 8           | Sales      | 65000  | 2    | 2          | 3          |
| 2           | IT         | 60000  | 1    | 1          | 1          |
| 3           | IT         | 60000  | 1    | 1          | 2          |
| 1           | IT         | 50000  | 3    | 2          | 3          |
| 5           | HR         | 55000  | 1    | 1          | 1          |
| 4           | HR         | 45000  | 2    | 2          | 2          |

Explanation:
RANK(): Assigns a rank to each row within the partition (department). If there are ties, the next rank is skipped. For example, in the IT department, employees with salaries of 60000 share the first rank (1), and the next employee gets rank 3.

DENSE_RANK(): Similar to `RANK`, but it does not skip ranks for ties. In the IT department, employees with salaries of 60000 both get rank 1, and the next employee gets rank 2.

ROW_NUMBER(): Assigns a unique number to each row within the partition. This is useful for scenarios where you need to uniquely identify each row within a group, even if there are ties in the ranking criteria.

### Question:

### Problem Statement

You are working as a data analyst for an e-commerce platform. The company is interested in analyzing product sales across different categories.
To gain insights, you have been asked to use SQL ranking functions to evaluate the performance of products based on their total sales.  

Schema:   
| Column Name    | Data Type     | Description                               |  
|----------------|---------------|-------------------------------------------|  
| category       | VARCHAR(50)   | The category to which the product belongs |  
| product_name   | VARCHAR(100)  | Name of the product                       |  
| total_sales    | INT           | Total sales for the product               |  

Task:  
1. Use the ranking functions to analyze product sales within each category:  
   - Rank products by total sales, allowing gaps for ties.  
   - Rank products sequentially, even for ties.  
   - Assign a unique number to each product, regardless of ties.  

2. Display these columns:  
   - category  
   - product_name
   - total_sales  
   - rnk, dense_rnk, and rn.  

3. Identify the top 3 products in each category using RANK().  
4. Compare the impact of ties on each ranking method.

### Schema setup

```sql
CREATE TABLE product_sales (
    category VARCHAR(50),
    product_name VARCHAR(100),
    total_sales INT
);

INSERT INTO product_sales (category, product_name, total_sales) VALUES  
('Electronics', 'Smartphone X', 5000),  
('Electronics', 'Laptop Y', 4500),  
('Electronics', 'Tablet Z', 4500),  
('Electronics', 'Smartwatch W', 3000),  
('Fashion', 'Sneakers A', 2000),  
('Fashion', 'Handbag B', 1800),  
('Fashion', 'Jacket C', 1700),  
('Fashion', 'Scarf D', 1600),  
('Home Appliances', 'Vacuum Cleaner E', 2500),  
('Home Appliances', 'Air Purifier F', 2300),  
('Home Appliances', 'Blender G', 2300),  
('Home Appliances', 'Microwave H', 2200);  
```

### Expected output

| category         | product_name      | total_sales | rnk | dense_rnk | rn |
|------------------|-------------------|-------------|-----|-----------|----|
| Electronics      | Smartphone X      | 5000        | 1   | 1         | 1  |
| Electronics      | Laptop Y          | 4500        | 2   | 2         | 2  |
| Electronics      | Tablet Z          | 4500        | 2   | 2         | 3  |
| Fashion          | Sneakers A        | 2000        | 1   | 1         | 1  |
| Fashion          | Handbag B         | 1800        | 2   | 2         | 2  |
| Fashion          | Jacket C          | 1700        | 3   | 3         | 3  |
| Home Appliances  | Vacuum Cleaner E  | 2500        | 1   | 1         | 1  |
| Home Appliances  | Air Purifier F    | 2300        | 2   | 2         | 2  |
| Home Appliances  | Blender G         | 2300        | 2   | 2         | 3  |

### Solution Query

```sql
Will Be Added Tommorrow
```
