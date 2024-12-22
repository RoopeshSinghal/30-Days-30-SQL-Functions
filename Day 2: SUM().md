## Day 2: SUM() 

The SQL SUM() function calculates the total sum of a numeric column.

# Syntax:

```sql
SELECT SUM(column_name) 
FROM table_name 
WHERE condition; 
```

# Example:
The following example returns the total sales amount of each product sold in the year 2003.

```sql
SELECT
     ProductID,
     SUM(SalesAmount) AS TotalPerProduct
FROM FactSales
WHERE OrderDate >= '2003-01-01'
      AND OrderDate < '2004-01-01'
GROUP BY ProductID
ORDER BY ProductID ;
```

# Question:
You are working with a transactions table that contains the following columns:

transaction_id INT: Unique ID for each transaction
transaction_date DATE: Date of the transaction
amount INT: Amount of the transaction

Write a SQL query to calculate the total revenue generated for each month in the last year. If no transactions occurred in a month, display that month with a total revenue of 0.

```sql
SELECT  
    MONTH(t.transaction_date) AS month,  
    COALESCE(SUM(t.amount), 0) AS total_revenue  
FROM transactions
WHERE YEAR(t.transaction_date) = YEAR(CURDATE()) - 1 
GROUP BY month
ORDER BY month;
```
