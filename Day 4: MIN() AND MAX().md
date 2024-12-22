## Day 4: MIN() AND MAX() 

The SQL MIN() and MAX() function returns the smallest value and largest value of the selected column respectively.

### Syntax:

```sql
SELECT MIN(column_name) / MAX(column_name)
FROM table_name 
WHERE condition; 
```

### Example:
The following example returns the customers whose age is greater than the minimum age and less than the maximum age in the Customers table.

```sql
SELECT *
FROM Customers
WHERE age > (SELECT MIN(age) FROM Customer)
AND age < (SELECT MAX(age) FROM Customer) ;
```

### Question:

### Problem Statement

You are working with a transactions table that contains the following columns:

transaction_id INT: Unique ID for each transaction
transaction_date DATE: Date of the transaction
amount INT: Amount of the transaction

Write a SQL query to determine the difference between the maximum and minimum transaction amounts for the current year.

### Schema setup

```sql
CREATE TABLE transactions (  
    transaction_id INT PRIMARY KEY,  
    transaction_date DATE NOT NULL,  
    amount INT NOT NULL  
);   

INSERT INTO transactions (transaction_id, transaction_date, amount) VALUES  
(1, '2024-01-15', 200),  
(2, '2024-02-20', 150),  
(3, '2024-03-10', 300),  
(4, '2024-04-25', 250),  
(5, '2024-05-05', 180),  
(6, '2024-06-14', 220),  
(7, '2024-07-19', 270),  
(8, '2024-08-09', 320),  
(9, '2024-09-12', 190),  
(10, '2024-10-08', 230),  
(11, '2024-11-18', 400),  
(12, '2024-12-05', 280),
(13, '2023-01-12', 210),  
(14, '2023-02-22', 180),  
(15, '2023-03-15', 290),  
(16, '2023-04-18', 260),  
(17, '2023-05-25', 170),  
(18, '2023-06-20', 300),  
(19, '2023-07-07', 310),  
(20, '2023-08-15', 220),  
(21, '2023-09-14', 400),  
(22, '2023-10-10', 230),  
(23, '2023-11-05', 310),  
(24, '2023-12-12', 280),  
(25, '2023-01-08', 250),  
(26, '2023-02-17', 310),  
(27, '2023-03-11', 200),  
(28, '2023-04-22', 180),  
(29, '2023-05-30', 190),  
(30, '2023-06-05', 320),  
(31, '2023-07-20', 270),  
(32, '2023-08-30', 290),  
(33, '2023-09-03', 210),  
(34, '2023-10-22', 240),  
(35, '2023-11-30', 260),  
(36, '2023-12-25', 300);  
```

### Solution Query

```sql
SELECT
   MAX(amount) - MIN(amount) AS amt_diff
FROM transactions
WHERE YEAR(transaction_date) =  YEAR(CURDATE());
```
