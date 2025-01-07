## Day 30: FIRST_VALUE() AND LAST_VALUE()

The FIRST_VALUE() and LAST_VALUE() window functions are used to retrieve the first and last values in a result set or within a partitioned window. These functions are beneficial for analyzing data trends and identifying starting and ending points.

1. FIRST_VALUE():
Returns the first value in a partition or result set based on the specified ordering.

2. LAST_VALUE():  
Returns the last value in a partition or result set based on the specified ordering.

### Syntax:

```sql
SELECT
  FIRST_VALUE / LAST_VALUE (column_name) OVER (PARTITION BY column_name ORDER BY column_name ASC/DESC)
FROM tablename;
```

### Example:

The following example demonstrates the use of First_value and Last_value 
for calculating the first and last sales for each product within a specific category

Imagine a table named `Product_Sales` with the following columns:  

- category: Product category  
- product_name: Name of the product  
- sales_month: Month of the sales  
- sales_units: Units sold in that month  

Input:  
| category    | product_name | sales_month | sales_units |  
|--------- ---|--------------|-------------|-------------|  
| Electronics | Laptop       | 2024-01-01  | 100         |  
| Electronics | Laptop       | 2024-02-01  | 150         |  
| Electronics | Laptop       | 2024-03-01  | 120         |  
| Electronics | Smartphone   | 2024-01-01  | 200         |  
| Electronics | Smartphone   | 2024-02-01  | 180         |  
| Electronics | Smartphone   | 2024-03-01  | 220         |  

```sql
SELECT  
    category,  
    product_name,  
    sales_month,  
    sales_units,  
    FIRST_VALUE(sales_units) OVER (PARTITION BY product_name ORDER BY sales_month) AS first_sales,  
    LAST_VALUE(sales_units) OVER (PARTITION BY product_name ORDER BY sales_month  
                                  ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS last_sales  
FROM  
    Product_Sales;  
```

Output:  
| category    | product_name | sales_month | sales_units | first_sales | last_sales |  
|--------- ---|--------------|-------------|-------------|-------------|------------|  
| Electronics | Laptop       | 2024-01-01  | 100         | 100         | 120        |  
| Electronics | Laptop       | 2024-02-01  | 150         | 100         | 120        |  
| Electronics | Laptop       | 2024-03-01  | 120         | 100         | 120        |  
| Electronics | Smartphone   | 2024-01-01  | 200         | 200         | 220        |  
| Electronics | Smartphone   | 2024-02-01  | 180         | 200         | 220        |  
| Electronics | Smartphone   | 2024-03-01  | 220         | 200         | 220        |  
   
### Question:

### Problem Statement

As a Data Analyst, your task is to identify the employees with the minimum and maximum overtime hours in the company.
This information will help the organization determine appropriate holiday allocations for each employee based on their workload.

Schema:
Table Name: Employee_Overtime  
| Column Name    | Data Type    | Description                                 |  
|----------------|--------------|---------------------------------------------|  
| employee_name  | VARCHAR(50)  | Name of the employee                        |  
| hours          | INT          | Total overtime hours worked by the employee |  

Task:

1. Display all employees' overtime hours.  
2. Find the employee with the least overtime hours and employee with the most overtime hours.  
3. Include the following columns in the output:  
   - employee_name  
   - hours
   - least_overtime_employee  
   - most_overtime_employee
  
### Schema setup

```sql
CREATE TABLE Employee_Overtime (
    employee_name VARCHAR(50),
    hours INT
);

INSERT INTO Employee_Overtime (employee_name, hours) VALUES
('Steve Patterson', 29),
('Diane Murphy', 37),
('Jeff Firrelli', 40),
('Gerard Bondur', 47),
('Loui Bondur', 49),
('William Patterson', 58),
('Barry Jones', 65),
('Foon Yue Tseng', 66),
('Anthony Bow', 66),
('Gerard Hernandez', 66),
('Mary Patterson', 74);
```

### Expected output

| employee_name       | hours | least_overtime_employee | most_overtime_employee |  
|---------------------|-------|-------------------------|------------------------|  
| Steve Patterson     | 29    | Steve Patterson         | Mary Patterson         |  
| Diane Murphy        | 37    | Steve Patterson         | Mary Patterson         |  
| Jeff Firrelli       | 40    | Steve Patterson         | Mary Patterson         |  
| Gerard Bondur       | 47    | Steve Patterson         | Mary Patterson         |  
| Loui Bondur         | 49    | Steve Patterson         | Mary Patterson         |  
| William Patterson   | 58    | Steve Patterson         | Mary Patterson         |  
| Barry Jones         | 65    | Steve Patterson         | Mary Patterson         |  
| Foon Yue Tseng      | 66    | Steve Patterson         | Mary Patterson         |  
| Anthony Bow         | 66    | Steve Patterson         | Mary Patterson         |  
| Gerard Hernandez    | 66    | Steve Patterson         | Mary Patterson         |  
| Mary Patterson      | 74    | Steve Patterson         | Mary Patterson         |  

### Solution Query

```sql
SELECT
    employee_name,
    hours,
    FIRST_VALUE(employee_name) OVER (ORDER BY hours ASC) AS least_overtime_employee,
    FIRST_VALUE(employee_name) OVER (ORDER BY hours DESC) AS most_overtime_employee
FROM
    Employee_Overtime;
```
