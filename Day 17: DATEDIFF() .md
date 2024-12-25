## Day 17: DATEDIFF()

The SQL `DATEDIFF()` function calculates the difference in days between two date values. It is widely used to determine the duration or interval between two dates, making it a valuable tool for analyzing time-based data.  

### Syntax:

```sql

SELECT DATEDIFF(date1, date2) AS difference_in_days;; 
```

• `date1`: The later date.  
<br>• `date2`: The earlier date.  

Returns: The number of days between `date1` and `date2`. 

### Example:

The following example demonstrated how to calculate the delivery time of each order.

Consider an `orders` table with the following data:  

| order_id | order_date  | delivery_date |  
|----------|-------------|---------------|  
| 1        | 2024-12-01  | 2024-12-05    |  
| 2        | 2024-12-03  | 2024-12-08    |  
| 3        | 2024-12-07  | 2024-12-10    |  

Task it to calculate the delivery time for each order:  

```sql
SELECT 
    order_id, 
    order_date, 
    delivery_date, 
    DATEDIFF(delivery_date, order_date) AS delivery_days
FROM orders;
```

Output:  
| order_id | order_date  | delivery_date | delivery_days |  
|----------|-------------|---------------|---------------|  
| 1        | 2024-12-01  | 2024-12-05    | 4             |  
| 2        | 2024-12-03  | 2024-12-08    | 5             |  
| 3        | 2024-12-07  | 2024-12-10    | 3             |  

### Question:

### Problem Statement

You are managing an employee leave tracking system for an organization. The `employee_leaves` table contains information about employees’ leave requests:  

| Column Name        | Data Type     | Description                                     |  
|--------------------|---------------|-------------------------------------------------|  
| leave_id           | INT           | Unique ID for each leave request                |  
| employee_id        | INT           | Unique ID for each employee                     |  
| leave_start_date   | DATE          | Start date of the leave                         |  
| leave_end_date     | DATE          | End date of the leave                           |  
| leave_status       | VARCHAR(20)   | Status of the leave (Approved/Rejected/Pending) |  

Task:  

1. Calculate the total leave duration (number of days) and the total number of approved leave requests for each employee based on their approved leaves.  
2. Determine whether an employee has exceeded their leave limit. If they have taken more than 10 days of leave, flag it as "Exceeded", otherwise flag it as "Not Exceeded".  
3. Display the following columns:  
   - `employee_id`  
   - `total_approved_days` (sum of all approved leave durations)  
   - `leave_count` (total number of approved leave requests)  
   - `leave_limit` (status indicating whether the leave limit was exceeded or not)   
   
### Schema setup

```sql
CREATE TABLE employee_leaves (
    leave_id INT,
    employee_id INT,
    leave_start_date DATE,
    leave_end_date DATE,
    leave_status VARCHAR(20)
);

INSERT INTO employee_leaves (leave_id, employee_id, leave_start_date, leave_end_date, leave_status) VALUES
(1, 101, '2024-01-01', '2024-01-10', 'Approved'),
(2, 101, '2024-06-15', '2024-06-20', 'Approved'),
(3, 102, '2024-02-05', '2024-02-08', 'Rejected'),
(4, 103, '2024-03-10', '2024-03-12', 'Approved'),
(5, 104, '2024-05-01', '2024-05-07', 'Approved'),
(6, 104, '2024-08-15', '2024-08-20', 'Approved'),
(7, 104, '2024-11-01', '2024-11-05', 'Approved'),
(8, 105, '2024-09-01', '2024-09-02', 'Pending');
```

### Expected output

| employee_id | total_approved_days  | leave_count | leave_limit    | 
|-------------|----------------------|-------------|----------------|
| 101         | 16                   | 2           |  Exceeded      |
| 103         |  3                   | 1           |  Not Exceeded  |             
| 104         | 18                   | 3           |  Exceeded      |

### Solution Query

```sql
Will be Added Tomorrow
```
