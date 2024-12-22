## Day 7: SUBSTRING() 

The SQL `SUBSTRING()` function extracts a part of a string based on a specified starting position and optional length. It is commonly used to retrieve specific portions of text from a column

### Syntax:

```sql
SELECT SUBSTRING(string, start_position, length); 
```
• `string`: The input string from which to extract.
<br>• `start_position`: The position (1-based index) where extraction starts. 
<br>• `length` (optional): The number of characters to extract. If omitted, the function returns all characters from the starting position to the end. 

### Example:

The following example demonstrates how to extract the first three characters of a product code.

```sql
SELECT SUBSTRING(product_code, 1, 3) AS ProductPrefix 
FROM products; 
```

### Question:

### Problem Statement

You are working with a `logs` table that contains the following columns:  

| Column Name  | Data Type   | Description                                                                               |  
|--------------|-------------|-------------------------------------------------------------------------------------------|  
| `log_id`     | INT         | Unique ID for each log entry                                                              |  
| `log_message`| VARCHAR(255)| A message that includes a timestamp in the format `YYYY-MM-DD HH:MM:SS - Message Content` |  
| `log_type`   | VARCHAR(50) | Type of the log (e.g., INFO, ERROR, WARNING)                                              |  

Write a query to:  
1. Extract the date (`YYYY-MM-DD`) from the `log_message` column.  
2. Extract the hour (`HH`) from the timestamp in the `log_message` column.  
3. Display the extracted date, extracted hour, and the `log_type` for all logs where the `log_type` is 'ERROR'.  

### Schema setup

```sql
CREATE TABLE logs (  
    log_id INT PRIMARY KEY,  
    log_message VARCHAR(255) NOT NULL,  
    log_type VARCHAR(50) NOT NULL  
);  

INSERT INTO logs (log_id, log_message, log_type) VALUES  
(1, '2024-12-14 15:45:23 - Database connection failed', 'ERROR'),  
(2, '2024-12-14 10:12:34 - User logged in', 'INFO'),  
(3, '2024-12-13 08:30:00 - Disk space running low', 'WARNING'),  
(4, '2024-12-13 22:18:11 - Unauthorized access attempt', 'ERROR'),  
(5, '2024-12-12 09:20:00 - Backup completed successfully', 'INFO'),  
(6, '2024-12-14 01:05:42 - Memory usage critical', 'ERROR'),  
(7, '2024-12-11 23:59:59 - Scheduled maintenance started', 'INFO'),  
(8, '2024-12-12 14:22:10 - Failed to save user preferences', 'ERROR'),  
(9, '2024-12-13 17:15:45 - API request timeout', 'ERROR'),  
(10, '2024-12-14 18:30:00 - Service unavailable due to high traffic', 'ERROR'),  
(11, '2024-12-12 11:45:20 - Email server connection lost', 'ERROR'),  
(12, '2024-12-11 03:55:15 - Data replication failure', 'ERROR');  
```

### Expected output

| Date       | Hour | log_type |
|------------|------|----------|
| 2024-12-11 | 3    | ERROR    |
| 2024-12-12 | 11   | ERROR    |
| 2024-12-12 | 14   | ERROR    |
| 2024-12-13 | 17   | ERROR    |
| 2024-12-13 | 22   | ERROR    |
| 2024-12-14 | 1    | ERROR    |
| 2024-12-14 | 15   | ERROR    |
| 2024-12-14 | 18   | ERROR    |

### Solution Query

```sql
SELECT
    DATE(CAST(SUBSTRING(log_message, 1, 19) AS DATETIME)) AS Date,
    HOUR(CAST(SUBSTRING(log_message, 1, 19) AS DATETIME)) AS Hour,
    log_type
FROM logs
WHERE log_type = 'ERROR'
ORDER BY Date, Hour;
```
