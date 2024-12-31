## Day 23: ABS()

The SQL `ABS()` function returns the absolute value of a number, removing any negative sign and ensuring a non-negative result. The function ensures that all values are positive by converting negative amounts to their absolute values, which is useful for standardizing profit or loss calculations

### Syntax:

```sql
SELECT ABS(number);
```

### Example:

The following example demonstrates the working of the `ABS()` function.  
  
Suppose you manage a financial system where you need to calculate the absolute profit or loss for transactions, regardless of whether the value is positive or negative.  

```sql
SELECT 
    transaction_id, 
    amount, 
    ABS(amount) AS absolute_value 
FROM 
    transactions;
```

Output:  
| transaction_id | amount  | absolute_value |  
|----------------|---------|----------------|  
| 1              | 500.75  | 500.75         |  
| 2              | -150.25 | 150.25         |  
| 3              | -300.00 | 300.00         |  
| 4              | 0       | 0.00           |  
| 5              | 1250.50 | 1250.50        |  

### Question:

### Problem Statement

You are managing a financial database for a company that tracks monthly gains and losses for various departments.
The `financial_records` table stores both positive and negative amounts, representing profits and losses, respectively.
The management wants a report that calculates the absolute value of these amounts to compare the total scale of transactions without considering whether they are gains or losses.

Schema:   
| Column Name      | Data Type    | Description                                      |  
|------------------|--------------|--------------------------------------------------|  
| record_id        | INT          | Unique ID for each financial record              |  
| department       | VARCHAR(50)  | Name of the department                           |  
| transaction_date | DATE         | Date of the transaction                          |  
| amount           | INT          | Amount of the transaction (positive or negative) |  

Task

1. Calculate the absolute value of the `amount` column to show the magnitude of transactions.  
2. Summarize the total absolute transaction amount for each department.  
3. Display the following columns:  
   - `department`  
   - `total_absolute_amount` (sum of absolute transaction amounts per department) 
   
### Schema setup

```sql
CREATE TABLE financial_records (
    record_id INT PRIMARY KEY,
    department VARCHAR(50),
    transaction_date DATE,
    amount DECIMAL(10,2)
);

INSERT INTO financial_records (record_id, department, transaction_date, amount) VALUES
(1, 'Sales', '2024-12-01', 500.00),
(2, 'Sales', '2024-12-05', -250.00),
(3, 'Sales', '2024-12-10', 400.00),
(4, 'Sales', '2024-12-15', -500.00),
(5, 'Marketing', '2024-12-02', -300.50),
(6, 'Marketing', '2024-12-08', 400.00),
(7, 'Marketing', '2024-12-12', -400.00),
(8, 'IT', '2024-12-03', 325.75),
(9, 'IT', '2024-12-09', -200.00),
(10, 'IT', '2024-12-14', -300.00);
```

### Expected output

| department      | total_absolute_amount |  
|-----------------|-----------------------|  
| Sales           | 1650.00               |  
| Marketing       | 1100.50               |  
| IT              | 825.75                |   

### Solution Query

```sql
Will Be Added Tomorrow
```
