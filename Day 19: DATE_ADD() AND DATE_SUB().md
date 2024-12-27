## Day 19: DATE_ADD() AND DATE_SUB()

The SQL `DATE_ADD()` and `DATE_SUB()` functions allow you to add or subtract specific intervals (such as days, months, or years) to or from a date value. These functions are useful for handling future or past date calculations in your database queries.

### Syntax:

```sql
SELECT DATE_ADD(date, INTERVAL value unit); 
```
Adds the specified interval to the given date.  

```sql
DATE_SUB(date, INTERVAL value unit); 
```
Subtracts the specified interval from the given date.

• date: Specified date to be modified.  
<br>• value unit :the value is the date or time interval to add or subtract. This value can be both positive and negative. And here the addunit is the type of interval to add such as SECOND, MINUTE, HOUR, DAY, YEAR, MONTH, etc. 

### Example:

This example demonstrates how to use the DATE_ADD and DATE_SUB functions to add and subtract various time intervals from a given date.

Let's assume we have a table named orders with a column order_date storing the date when each order was placed. We want to:

Find the orders placed within the last 7 days.
Calculate the expected delivery date for orders, assuming a standard delivery time of 5 business days.

```sql
SELECT
    order_id,
    order_date,
    DATE_ADD(order_date, INTERVAL 5 DAY) AS expected_delivery_date,
    CASE
        WHEN order_date >= DATE_SUB(CURDATE(), INTERVAL 7 DAY) THEN 'Within Last 7 Days'
        ELSE 'Older Than 7 Days'
    END AS order_status
FROM orders;
```

### Question:

### Problem Statement

A hotel chain is looking to analyze its room sales performance during the 2024 holiday season.
The goal is to gain insights into booking trends in the lead-up to Christmas and during the period between Christmas and New Year's Day.
By understanding these trends, the hotel can optimize its sales strategies during peak holiday periods.

Schema:
| Column Name   | Data Type    | Description                                              |
|---------------|--------------|----------------------------------------------------------|
| booking_id    | INT          | Unique identifier for each booking (Primary Key).       |
| room_type     | VARCHAR(10)  | Type of room booked (e.g., Single, Double).             |
| booking_date  | DATE         | The date when the booking was made.                      |
| year          | INT          | The year in which the booking was made (e.g., 2024).     |

Task:

The hotel chain wants to analyze its room bookings during two specific holiday periods:

1. Bookings made within 14 days before Christmas (December 25th, 2024).
2. Bookings made between Christmas (December 25th, 2024) and New Year's Day (January 1st, 2025).

The task is to identify the number of bookings made in each of these two timeframes.
This will allow the hotel to analyze sales performance and adjust their strategy accordingly during the holiday season.
   
### Schema setup

```sql
CREATE TABLE Bookings (
    booking_id INT PRIMARY KEY,
    room_type VARCHAR(10),
    booking_date DATE,
    year INT
);

INSERT INTO Bookings (booking_id, room_type, booking_date, year) VALUES
(1, 'Single', '2024-12-11', 2024),
(2, 'Double', '2024-12-12', 2024),
(3, 'Suite', '2024-12-15', 2024),
(4, 'Single', '2024-12-12', 2024),
(5, 'Double', '2024-12-22', 2024),
(6, 'Suite', '2024-12-20', 2024),
(7, 'Single', '2024-12-25', 2024),
(8, 'Double', '2024-12-26', 2024),
(9, 'Suite', '2024-12-18', 2024),
(10, 'Single', '2024-12-22', 2024),
(11, 'Double', '2024-12-19', 2024),
(12, 'Suite', '2024-12-21', 2024),
(13, 'Single', '2024-12-20', 2024),
(14, 'Double', '2024-12-17', 2024),
(15, 'Suite', '2024-12-24', 2024),
(16, 'Single', '2024-12-14', 2024),
(17, 'Double', '2024-12-11', 2024),
(18, 'Suite', '2024-12-27', 2024),
(19, 'Single', '2024-12-16', 2024),
(20, 'Double', '2024-12-23', 2024),
(21, 'Single', '2024-12-27', 2024),
(22, 'Double', '2024-12-28', 2024),
(23, 'Suite', '2024-12-30', 2024);
```

### Expected output

| booking_period                | booking_count |
|-------------------------------|---------------|
| Before 14 Days of Christmas   | 17            |
| Between Christmas & New Year  | 6             |

### Solution Query

```sql
Will be Added Tomorrow
```
