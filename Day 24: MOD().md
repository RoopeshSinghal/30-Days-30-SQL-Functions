## Day 24: MOD() 

The SQL `MOD()` function  or % modulo operator calculates the remainder when one number is divided by another. It is often used for tasks like identifying even or odd numbers, cycling through records, or distributing workloads evenly.

### Syntax:

```sql
SELECT MOD(dividend, divisor);
```

• The dividend i.e.  a  number or a numeric expression that will be divided by divisor.
<br>• The divisor i.e. a number or a numeric expression by which to divide the dividend.

### Example:

Identifying Even and Odd Numbers  
The following example demonstrates checking whether numbers are even or odd.

```sql
SELECT number, 
       MOD(number, 2) AS remainder,
       CASE 
           WHEN MOD(number, 2) = 0 THEN 'Even' 
           ELSE 'Odd' 
       END AS number_type
FROM (SELECT 1 AS number UNION SELECT 2 UNION SELECT 3 UNION SELECT 4) AS numbers;
```

Output:  
| number | remainder | number_type |  
|--------|-----------|-------------|  
| 1      | 1         | Odd         |  
| 2      | 0         | Even        |  
| 3      | 1         | Odd         |  
| 4      | 0         | Even        |   

### Question:

### Problem Statement

You are managing an e-commerce system where each order has a unique `order_id`.

To streamline delivery and logistics, the orders are categorized into two groups based on their `order_id`:  
1. Even Group: Orders with an even `order_id`.  
2. Odd Group: Orders with an odd `order_id`.  

Additionally, calculate the percentage of total orders in each group (Even and Odd) to understand the distribution of orders.

Schema:
| Column Name      | Data Type    | Description                             |
|------------------|--------------|-----------------------------------------|
| `order_id`       | INT          | Unique ID for each order                |
| `customer_name`  | VARCHAR(50)  | Name of the customer placing the order  |
| `order_date`     | DATE         | The date the order was placed           |
| `total_amount`   | INT          | Total value of the order                |

Task  
1. Create a query to classify each order into "Even Group" or "Odd Group" based on the `order_id`.  
2. Calculate the percentage of total orders in each group.  
3. Display the following columns:  
   - `order_id`  
   - `customer_name`  
   - `order_date`  
   - `total_amount`  
   - `order_group` (either "Even Group" or "Odd Group").  
4. Additionally, display the total count and percentage for each group.
   
### Schema setup

```sql
CREATE TABLE orders (
    order_id INT,
    customer_name VARCHAR(50),
    order_date DATE,
    total_amount INT
);

INSERT INTO orders (order_id, customer_name, order_date, total_amount) VALUES
(1, 'Alice Johnson', '2023-12-01', 120.50),
(2, 'Bob Smith', '2023-12-02', 99.99),
(3, 'Charlie Brown', '2023-12-03', 49.00),
(4, 'Daisy Miller', '2023-12-04', 200.75),
(5, 'Ethan Davis', '2023-12-05', 150.00),
(6, 'Fiona Williams', '2023-12-06', 250.00);
```

### Expected output

| order_group | group_count | group_percentage |  
|-------------|-------------|------------------|  
| Even Group  | 3           | 50.00%           |  
| Odd Group   | 3           | 50.00%           |

### Solution Query

```sql
Will Be Added Tomorrow
```
