## Day 20: CURRENT_DATE(), CURRENT_TIME() AND CURRENT_TIMESTAMP()

The MySQL functions CURRENT_DATE, CURRENT_TIME, and CURRENT_TIMESTAMP provide the current date, time, or both respectively. These functions are useful for tracking timestamps, setting default values, or filtering data based on real-time conditions.

### Syntax:

• CURRENT_DATE
Returns the current date in YYYY-MM-DD format.
```sql
SELECT CURRENT_DATE();
```

• CURRENT_TIME
Returns the current time in HH:MM:SS format.
```sql
SELECT CURRENT_TIME();
```

• CURRENT_TIMESTAMP or NOW()
Returns the current date and time in YYYY-MM-DD HH:MM:SS format.
```sql
SELECT CURRENT_TIMESTAMP()/ NOW();
```

### Examples:

The following examples illustrate how to extract the current date and time:

Example 1:
Getting the current date.
```sql
SELECT CURRENT_DATE AS Today;
```
Output:
| Today      |
|------------|
| 2024-12-28 |

Example 2:
Getting the current time.
```sql
SELECT CURRENT_TIME AS CurrentTime;
```
Output:
| CurrentTime |
|-------------|
| 05:32:10    |

Example 3:
Getting the current timestamp.
```sql
SELECT CURRENT_TIMESTAMP AS CurrentTimestamp;
```
Output:
| CurrentTimestamp    |
|---------------------|
| 2024-12-28 05:32:10 | 

### Question:

### Problem Statement

You are managing an e-commerce platform that tracks customer orders. One of the critical tasks is monitoring the processing times for orders that are still pending.
To ensure timely delivery and customer satisfaction, you need to analyze the time elapsed since each pending order was placed

Schema:
| Column Name      | Data Type     | Description                             |  
|------------------|---------------|-----------------------------------------|  
| order_id         | INT           | Unique ID for each order                |  
| order_date       | DATETIME      | Date and time when the order was placed |  
| order_status     | VARCHAR(20)   | Current status of the order             |  

Task:

Write a query to:

1. Display the order_id and order_date for all pending orders.
2. Display the current date and time.
3. Compute the number of hours that have passed since the order_date.
4. Display the following columns:
    - order_id: Unique identifier for the order.
    - order_date: Date and time when the order was placed.
    - current_time: The current date and time.
    - hours_since_order: Total hours elapsed since the order was placed.

This will help the manager identify delayed orders and take appropriate actions to expedite processing.
   
### Schema setup

```sql
CREATE TABLE orders (
    order_id INT,
    order_date DATETIME,
    order_status VARCHAR(20)
);

INSERT INTO orders (order_id, order_date, order_status) VALUES
(1, '2024-12-25 10:00:00', 'Pending'),
(2, '2024-12-24 08:30:00', 'Completed'),
(3, '2024-12-23 14:45:00', 'Pending'),
(4, '2024-12-25 15:00:00', 'Shipped');
```

### Expected output

| order_id | order_date          | current_time        | hours_since_order |  
|----------|---------------------|---------------------|-------------------|  
| 1        | 2024-12-25 10:00:00 | 2024-12-28 05:45:02 | 67                |  
| 3        | 2024-12-23 14:45:00 | 2024-12-28 05:45:02 | 111               |  

Note: The Expected Output can vary due to the change in time!!

### Solution Query

```sql
Will Be Added Tomorrow
```
