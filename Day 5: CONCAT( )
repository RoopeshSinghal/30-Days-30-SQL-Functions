## Day 5: CONCAT() 

The SQL CONCAT() function returns a string resulting from the concatenation, or joining, of two or more string values in an end-to-end manner.

### Syntax:

```sql
SELECT CONCAT(string1, string2, ...., string_n) ;
```

### Example:
The following example demonstrates how to concatenate an employee's full name.

```sql
SELECT CONCAT(emp_name," ",emp_middlename," ",emp_lastname) AS FullName
FROM emp;
```

### Question:

### Problem Statement

You have a table orders with the following columns:

order_id (INT)
customer_name (VARCHAR)
order_date (DATE)
total_amount (DECIMAL)
status (VARCHAR: values can be "Pending", "Completed", "Canceled")


Write a query to create a detailed summary for each order in the following format:
Order Summary: Order #[order_id] by [customer_name] on [formatted_order_date] - [status]. Total: $[total_amount_formatted]

Additional Requirements:

1. Format the order_date as Month Day, Year (e.g., December 5, 2023).
2. Round total_amount to two decimal places and ensure it is prefixed with a dollar sign ($).
3. Replace any NULL values in customer_name or status with "Unknown".


### Schema setup

```sql
CREATE TABLE orders(
order_id INT,
customer_name VARCHAR(20),
order_date DATE,
total_amount INT,
status VARCHAR(20)
);

INSERT INTO orders (order_id, customer_name, order_date, total_amount, status)  
VALUES  
(101, 'John Doe', '2023-12-05', 150, 'Completed'),  
(102, 'Damon Salvatore', '2023-11-20', 121, 'Pending'),
(103, 'Arun Singh', '2023-08-08', 101, 'Canceled'); 
```

### Expected output

| order_summary                                                                             |
|-------------------------------------------------------------------------------------------|
| Order Summary: Order #101 by John Doe on December 05, 2023 - Completed. Total: $150       |
| Order Summary: Order #102 by Damon Salvatore on November 20, 2023 - Pending. Total: $121  |
| Order Summary: Order #103 by Arun Singh on August 08, 2023 - Canceled. Total: $101        |

### Solution Query

```sql
SELECT 
    CONCAT(
        'Order Summary: Order #', order_id, 
        ' by ', COALESCE(customer_name, 'Unknown'), 
        ' on ', DATE_FORMAT(order_date, '%M %d, %Y'), 
        ' - ', COALESCE(status, 'Unknown'), 
        '. Total: $', total_amount
    ) AS order_summary
FROM orders;
```
