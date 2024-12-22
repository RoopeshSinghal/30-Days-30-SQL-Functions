## Day 6: CAST()

The SQL `CAST()` function converts a value from one data type to another. It is often used to transform data for calculations, comparisons, or formatting in queries. 

### Syntax:

```sql
SELECT CAST(expression AS target_data_type) ;
```

### Examples:

The following example demonstrates how to convert a numerical value into a string.
```sql
SELECT CAST(12345 AS CHAR) AS ConvertedValue ;
```

The following example demonstrates how to convert a value to a DATE datatype.
```sql
SELECT CAST("2017-08-29" AS DATE) AS ConvertedValue ; 
```

### Question:

### Problem Statement

You are working with a sales table that contains the following columns:

sale_id	INT: Unique identifier for each sale
sale_date DATE:	The date when the sale occurred
sale_amount	VARCHAR: Sale amount stored as a string
discount_rate VARCHAR: Discount rate stored as a percentage string
    
The sale_amount and discount_rate columns are stored as strings due to legacy system constraints.
Your task is to calculate the net revenue for each sale by performing the following:

1. Convert sale_amount to a numeric value.
2. Convert discount_rate to a decimal value.
3. Apply the discount to the sale amount.
4. Return the sale_id, sale_date, net_revenue, and round the net_revenue to 2 decimal places.
    
Additionally, filter the results to only include sales that occurred in the current month

### Schema setup

```sql
CREATE TABLE sales (  
    sale_id INT PRIMARY KEY,  
    sale_date DATE NOT NULL,  
    sale_amount VARCHAR(10) NOT NULL,  
    discount_rate VARCHAR(5) NOT NULL  
);  

INSERT INTO sales (sale_id, sale_date, sale_amount, discount_rate) VALUES  
(1, '2024-12-01', '1500', '10%'),  
(2, '2024-12-05', '2000', '5%'),  
(3, '2024-11-25', '3000', '15%'),  
(4, '2024-12-10', '500', '20%'),  
(5, '2024-12-12', '1200', '12%'),  
(6, '2024-11-15', '800', '0%'),  
(7, '2024-12-20', '2500', '8%');  
```

### Expected output

| sale_id | sale_date   | net_revenue |
|---------|-------------|-------------|
| 1       | 2024-12-01  | 1350.00     |
| 2       | 2024-12-05  | 1900.00     |
| 4       | 2024-12-10  | 400.00      |
| 5       | 2024-12-12  | 1056.00     |
| 7       | 2024-12-20  | 2300.00     |

### Solution Query

```sql
SELECT  
    sale_id,  
    sale_date,  
    ROUND(CAST(sale_amount AS DECIMAL(10, 2)) * (1 - CAST(REPLACE(discount_rate, '%', '') AS DECIMAL(5, 2)) / 100), 2) AS net_revenue  
FROM sales  
WHERE MONTH(sale_date) = MONTH(CURDATE())  
  AND YEAR(sale_date) = YEAR(CURDATE());
```
