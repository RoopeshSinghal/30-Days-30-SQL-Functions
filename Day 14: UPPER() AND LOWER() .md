## Day 14: UPPER() AND LOWER() 

The SQL `UPPER()` function converts all characters in a string to uppercase, while the `LOWER()` function converts all characters in a string to lowercase. These functions are often used for case-insensitive comparisons or standardizing text formats.

### Syntax:

UPPER()/UCASE() Function:
```sql
SELECT UPPER(string) AS uppercased_string;
```

LOWER()/LCASE() Function:
```sql
SELECT LOWER(string) AS lowercased_string;
```

### Example:

The following example demonstrates how to convert the text in "first_name" to upper-case and the text in "last_name" to lower-case.

| user_id | first_name | last_name | 
|---------|------------|-----------|
| 1       | Alice      | Johnson   |
| 2       | BOB        | SMITH     |
| 3       | Carol      | Brown     |

```sql
SELECT 
 UPPER(first_name) AS upper_case_first_name,
 LOWER(last_name) AS lower_case_last_name
FROM users;
```

| upper_case_first_name | lower_case_last_name |
|-----------------------|----------------------|
| ALICE                 | johnson              |
| BOB                   | smith                |
| CAROL                 | brown                |

### Question:

### Problem Statement

You manage a product catalog for an e-commerce platform. The `products` table stores product names and descriptions in mixed case. You need to ensure data consistency and extract specific insights based on standardized formats.  

| Column Name         | Data Type        | Description                                       |
|---------------------|------------------|---------------------------------------------------|
| product_id          | INT              | Unique identifier for each product (Primary Key). |
| product_name        | VARCHAR(255)     | Name of the product.                              |
| product_description | TEXT             | Detailed description of the product.              |
| price               | DECIMAL(10, 2)   | Price of the product.                             |

Task:

1. Convert all product names to uppercase using the `UPPER()` function.  
2. Convert all product descriptions to lowercase using the `LOWER()` function.While keeping the first letter in caps
3. Filter and display only products where the product name contains the word "LAPTOP" (case-insensitively).  
4. Include the following columns in the result:  
   - `product_id`  
   - `product_name` (uppercase format)  
   - `product_description` (lowercase format)  
   - `price`  
   
### Schema setup

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(255),
    product_description TEXT,
    price DECIMAL(10, 2)
);

INSERT INTO products (product_id, product_name, product_description, price) VALUES
(1, 'Gaming Laptop', 'High performance laptop with RGB keyboard', 1200.00),
(2, 'Office Laptop', 'Designed for office productivity and light gaming', 850.00),
(3, 'Gaming Mouse', 'Ergonomic mouse with customizable buttons', 50.00),
(4, 'Laptop Stand', 'Durable and lightweight stand for laptops', 30.00),
(5, 'Wireless Earbuds', 'Noise-cancelling earbuds with long battery life', 100.00),
(6, 'Ultrabook Laptop', 'Slim and portable laptop with long battery life', 1500.00),
(7, 'Tablet', '10-inch screen tablet with powerful performance', 300.00);
```

### Expected output

| product_id | product_name_upper   | product_description_lower                                  | price    |  
|------------|----------------------|------------------------------------------------------------|----------|  
| 1          | GAMING LAPTOP        | high performance laptop with rgb keyboard                  | 1200.00  |  
| 2          | OFFICE LAPTOP        | designed for office productivity and light gaming          | 850.00   |  
| 4          | LAPTOP STAND         | durable and lightweight stand for laptops                  | 30.00    |  
| 6          | ULTRABOOK LAPTOP     | slim and portable laptop with long battery life            | 1500.00  |  

### Solution Query

```sql
SELECT
    product_id,
    UPPER(product_name) AS product_name_upper,
    CONCAT(UPPER(LEFT(product_description,1)),'',LOWER(SUBSTRING(product_description,2,LENGTH(product_description)))) AS product_description_lower,
    price
FROM products;
```
