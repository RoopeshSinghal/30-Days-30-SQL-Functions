## Day 8: TRIM() 

The SQL `TRIM()` function removes unwanted spaces or specified characters from the beginning, end, or both sides of a string. This is particularly useful for cleaning up user input or data imports where strings may have extra spaces.

### Syntax:

```sql
SELECT TRIM([{BOTH | LEADING | TRAILING} [remstr] FROM] str) ; 
```
• BOTH | LEADING | TRAILING : LEADING, TRAILING, or BOTH option to explicitly instruct the TRIM() function to remove leading, trailing, or both leading and trailing unwanted characters from a string .By default, the TRIM() function uses the BOTH option.
<br>• removed_str : It is a string which we want to remove. If not given, spaces will be removed.
<br>• str : It identifies the string from which we want to remove removed_str.

### Example:

The following example demonstrates how to remove extra spaces from a product name.
```sql
SELECT TRIM(BOTH ' ' FROM ' Apple iPhone 15 ') AS CleanedName; 
```
| CleanedName     |
|-----------------|
| Apple iPhone 15 |

### Question:


### Problem Statement

You are working with a `products` table that contains the following columns:  

| Column Name   | Data Type | Description                                                                  |  
|---------------|-----------|------------------------------------------------------------------------------|  
| `product_id`  | INT       | Unique ID for each product                                                   |  
| `product_name`| VARCHAR   | Product names that may have leading and trailing spaces or underscores (`_`) |  
| `price`       | INT       | Price of the product                                                         |  

Task:  
Write a query to:  
1. Remove leading and trailing underscores (`_`) and spaces from the `product_name` column using only the `TRIM()` function.  
2. Display the cleaned `product_name` along with `product_id` and `price`.

Sample Input (products table):  
| product_id | product_name        | price    |  
|------------|---------------------|----------|  
| 1          | __Laptop__          | 800.00   |  
| 2          |  Smartphone_        | 600.00   |  
| 3          | __Tablet            | 300.00   |  
| 4          |  Keyboard           | 50.00    |  

### Schema setup

```sql
CREATE TABLE products (
    product_id INT,
    product_name VARCHAR(15),
    price INT
);

INSERT INTO products (product_id, product_name, price) VALUES
(1, '__Laptop__', 800.00),
(2, ' Smartphone_', 600.00),
(3, '__Tablet', 300.00),
(4, ' Keyboard ', 50.00),
(5, '__Monitor__', 250.00),
(6, ' Headphones_', 120.00),
(7, '  Mouse  ', 30.00);
```

### Expected output

| product_id | cleaned_product_name  | price    |  
|------------|-----------------------|----------|  
| 1          | Laptop                | 800.00   |  
| 2          | Smartphone            | 600.00   |  
| 3          | Tablet                | 300.00   |  
| 4          | Keyboard              | 50.00    |  

### Solution Query

```sql
SELECT
    product_id,
    TRIM(BOTH ' ' FROM (TRIM(BOTH '_' FROM product_name))) AS cleaned_product_name,
    price
FROM products;
```
