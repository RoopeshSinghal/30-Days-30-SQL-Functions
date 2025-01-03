## Day 26: SQRT()

The SQRT() function in SQL is used to calculate the square root of a given number.

### Syntax:

```sql
SELECT SQRT(number);   
```

### Example:

The example demonstrates how square root function can be used for
analyzing customer purchase behavior

A company like Amazon wants to analyze customer purchase behavior to identify trends and patterns.

To analyze the purchase behavior, they want to calculate the square root of the average order total for each customer. This can help them identify customers who make consistent purchases.

Input:
| customer_id | order_total | order_date |
|-------------|-------------|------------|
| 1           | 100         | 2022-01-01 |
| 1           | 120         | 2022-01-15 |
| 1           | 90          | 2022-02-01 |
| 2           | 50          | 2022-01-05 |
| 2           | 75          | 2022-01-20 |
| 3           | 200         | 2022-01-10 |
| 3           | 250         | 2022-02-15 |

```sql
SELECT
   customer_id,
   SQRT(AVG(order_total)) AS avg_order_total_sqrt
FROM orders
GROUP BY customer_id;
```

Output:
| customer_id | avg_order_total_sqrt |
|-------------|--------------- ------|
| 1           | 10.39                |
| 2           | 8.66                 |
| 3           | 15.81                |

This query calculates the square root of the average order total for each customer, providing valuable insights into customer purchase behavior.

### Question:

### Problem Statement

You are a data analyst working for a logistics company.
Your task is to analyze the delivery time efficiency of the delivery agents.
The company's database contains a table named `deliveries`, which has the following schema:  

Schema:  
| Column Name         |   Data Type   | Description                                          |  
|---------------------|---------------|------------------------------------------------------|  
| delivery_id         | INT           | Unique ID for each delivery                          |  
| agent_name          | VARCHAR(15)   | Name of the delivery agent                           |  
| total_distance_km   | INT           | Total distance covered for the delivery (in km)      |  
| total_time_hours    | INT           | Total time taken to complete the delivery (in hours) |  
| delivery_status     | VARCHAR(10)   | Status of the delivery (Completed/Delayed/Failed)    |  

Task:
1. Calculate the efficiency score for each delivery as the square root of the total distance divided by the total time.  
2. Identify the top-performing delivery agents based on their efficiency scores, where the efficiency score is greater than 2.  
3. Display the following columns:  
   - `delivery_id`  
   - `agent_name`  
   - `efficiency_score`  
   - `delivery_status`  
   
### Schema setup

```sql
CREATE TABLE deliveries (  
    delivery_id INT,  
    agent_name VARCHAR(15),  
    total_distance_km INT,  
    total_time_hours INT,  
    delivery_status VARCHAR(10)  
);  

INSERT INTO deliveries (delivery_id, agent_name, total_distance_km, total_time_hours, delivery_status) VALUES  
(1, 'John Doe', 50, 10, 'Completed'),  
(2, 'Jane Roe', 40, 12, 'Delayed'),  
(3, 'Mike Brown', 60, 30, 'Failed'),  
(4, 'Emily Smith', 80, 18, 'Completed'),  
(5, 'Chris Adams', 100, 60, 'Delayed'),  
(6, 'Anna Taylor', 90, 50, 'Completed');  
```

### Expected output

| delivery_id | agent_name   | efficiency_score | delivery_status |  
|-------------|--------------|------------------|-----------------|  
| 1           | John Doe     | 2.24             | Completed       |  
| 4           | Emily Smith  | 2.12             | Completed       | 

### Solution Query

```sql
Will Be Added Tomorrow
```
