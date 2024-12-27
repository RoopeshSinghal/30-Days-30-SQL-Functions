## Day 18: DATE_FORMAT()

The SQL `DATE_FORMAT()` function is used to format date or datetime values into a specified string format. It allows you to customize the display of date and time values in various ways using format specifiers.
### Syntax:

```sql
SELECT DATE_FORMAT(date, format); 
```
• `date`: The date or datetime value to be formatted.<br>
• `format`: A string defining the format of the output.<br>
  Common format specifiers include:
   - `%Y`: Year (4 digits)
   - `%m`: Month (2 digits)
   - `%b`: Abbreviated month name
   - `%d`: Day of the month (2 digits)
   - `%H`: Hour (24-hour format)
   - `%i`: Minutes
   - `%s`: Seconds

### Examples:

The following examples illustrate how to format and extract the order_date in various ways, such as converting it to different date formats or extracting specific components like year, month, and day:

Example 1:
Getting a formatted year from the specified date 2020-11-23.
```sql
SELECT DATE_FORMAT("2020-11-23", "%Y") AS formatted_year;
```
Output:
formatted_year
2020

Example 2:
Getting a formatted month name from the specified date 2020-11-23.
```sql
SELECT DATE_FORMAT("2020-11-23", "%M") AS formatted_month;
```
Output:
formatted_month
November

Example 3:
Getting a day of the month from the specified date 2020-11-23.
```sql
SELECT DATE_FORMAT("2020-11-23", "%D") AS formatted_day;
```
Output:
formatted_day
23rd

Example 4:
Getting the month, day, and year from the specified date 2020-11-23.
```sql
SELECT DATE_FORMAT("2020-11-23", "%M %d %Y") AS formatted_date;
```
Output:
formatted_date
November 23 2020 

### Question:

### Problem Statement

You are managing a hotel booking system. The `bookings` table stores information about customer bookings, including check-in and check-out dates. The goal is to generate a summary of bookings for a monthly report. The report should format the dates and display useful information.

Schema:  
| Column Name       | Data Type   | Description                          |  
|-------------------|-------------|--------------------------------------|  
| booking_id        | INT         | Unique ID for each booking           |  
| customer_name     | VARCHAR(20) | Name of the customer                 |  
| check_in_date     | DATE        | Check-in date of the booking         |  
| check_out_date    | DATE        | Check-out date of the booking        |  
| total_amount      | INT         | Total amount charged for the booking |  

Task:
 
1. Format the `check_in_date` and `check_out_date` as "Day Month Year" (e.g., "20th December 2024").  
2. Calculate the number of nights between `check_in_date` and `check_out_date`.
3. Calculate the month Difference between `check_in_date` and `check_out_date`.
4. Include the following columns in the result:  
   - `booking_id`  
   - `customer_name`  
   - `formatted_check_in`  
   - `formatted_check_out`  
   - `nights_stayed`  
   - `month_diff` 
   - `total_amount` 
   
### Schema setup

```sql
CREATE TABLE bookings (
    booking_id INT PRIMARY KEY,
    customer_name VARCHAR(20),
    check_in_date DATE,
    check_out_date DATE,
    total_amount DECIMAL(8,2)
);

INSERT INTO bookings (booking_id, customer_name, check_in_date, check_out_date, total_amount) VALUES
(1, 'Alice Johnson', '2024-11-20', '2024-12-25', 500.00),
(2, 'Bob Smith', '2024-10-10', '2024-12-12', 200.00),
(3, 'Charlie Brown', '2024-12-05', '2024-12-10', 450.00),
(4, 'Diana Prince', '2024-12-15', '2024-12-20', 600.00),
(5, 'Ethan Hunt', '2024-09-18', '2024-12-22', 400.00);
```

### Expected output

| booking_id | customer_name   | formatted_check_in     | formatted_check_out    | nights_stayed | month_diff | total_amount |
|------------|-----------------|------------------------|------------------------|---------------|------------|--------------|
| 1          | Alice Johnson   | 20th November 2024     | 25th December 2024     | 35            | 1          | 500.00       |
| 2          | Bob Smith       | 10th October 2024      | 12th December 2024     | 63            | 2          | 200.00       |
| 3          | Charlie Brown   | 5th December 2024      | 10th December 2024     | 5             | 0          | 450.00       |
| 4          | Diana Prince    | 15th December 2024     | 20th December 2024     | 5             | 0          | 600.00       |
| 5          | Ethan Hunt      | 18th September 2024    | 22nd December 2024     | 95            | 3          | 400.00       |

### Solution Query

```sql
SELECT 
    booking_id,
    customer_name,
    DATE_FORMAT(check_in_date, '%D %M %Y') AS formatted_check_in,
    DATE_FORMAT(check_out_date, '%D %M %Y') AS formatted_check_out,
    DATEDIFF(check_out_date, check_in_date) AS nights_stayed,
    DATE_FORMAT(check_out_date, '%m') - DATE_FORMAT(check_in_date, '%m') AS month_diff,
    total_amount
FROM bookings;
```
