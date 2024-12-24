## Day 13: LEFT() and RIGHT()

The SQL LEFT() and RIGHT() functions extract a specified number of characters from the left or right side of a string, respectively.

### Syntax:

LEFT() Function:
```sql
SELECT LEFT(column_name, number_of_characters)
FROM table_name;
```

RIGHT() Function:
```sql
SELECT RIGHT(column_name, number_of_characters)
FROM table_name;
```

### Example:

The following example demonstrates how to extract the prefix and unique identifier from the product serial numbers.

```sql
SELECT 
 product_id, 
 serial_number, 
 LEFT(serial_number, 3) AS product_prefix, 
 RIGHT(serial_number, 4) AS unique_id
FROM products;
```

| product_id | serial_number | product_prefix | unique_id |
|------------|---------------|----------------|-----------|
| 1          | CAT12345      | CAT            | 2345      |
| 2          | ELE98765      | ELE            | 8765      |
| 3          | HME45678      | HME            | 5678      |

### Question:

### Problem Statement

You manage an online event ticketing system where each ticket has a unique Ticket Code in the following format:  
`<priority_code><region_code><ticket_number>`
 
• `priority_code`: First 3 characters (e.g., "HIG", "MED", "LOW").  
<br>• `region_code`: The next 2 characters (e.g., "NA", "EU", "AP").  
<br>• `ticket_number`: Remaining digits after the region code.

| Column Name   | Data Type     | Description                                         |
|---------------|---------------|-----------------------------------------------------|
| ticket_id     | INT           | Unique identifier for each ticket (Primary Key).   |
| ticket_title  | VARCHAR(255)  | Title or brief description of the ticket.          |
| ticket_code   | VARCHAR(50)   | Unique alphanumeric code assigned to the ticket.   |
| ticket_status | VARCHAR(20)   | Status of the ticket (e.g., Open, Resolved).       |

Task:
Write a query using only `LEFT()` and `RIGHT()` to:

1. Extract the priority_code (the first 3 characters).  
2. Extract the region_code (the 4th and 5th characters).  
3. Extract the ticket_number (all remaining digits after the first 5 characters).  
4. Display tickets where:  
   • `priority_code` is "HIG".  
   • `ticket_number` is greater than 6000.  
   
### Schema setup

```sql
CREATE TABLE event_tickets (
    ticket_id INT PRIMARY KEY,
    ticket_title VARCHAR(255),
    ticket_code VARCHAR(50),
    ticket_status VARCHAR(20)
);

INSERT INTO event_tickets (ticket_id, ticket_title, ticket_code, ticket_status) VALUES
(1, 'VIP Access Pass Issue', 'HIGNA7001', 'Open'),
(2, 'Standard Seat Reservation Error', 'LOWEU4500', 'Resolved'),
(3, 'Premium Seat Upgrade Issue', 'HIGAP6502', 'Open'),
(4, 'General Admission Issue', 'MEDNA3200', 'Closed'),
(5, 'VIP Parking Pass Not Valid', 'HIGEU8005', 'Open'),
(6, 'Ticket Cancellation Problem', 'LOWNA2001', 'Resolved'),
(7, 'Payment Processing Delay', 'MEDAP3400', 'Closed'),
(8, 'Invalid QR Code Scanned', 'HIGNA6100', 'Resolved');
```

### Expected output

| ticket_id | ticket_title                | priority_code | region_code | ticket_number | ticket_status |  
|-----------|-----------------------------|---------------|-------------|---------------|---------------|  
| 1         | VIP Access Pass Issue       | HIG           | NA          | 7001          | Open          |  
| 3         | Premium Seat Upgrade Issue  | HIG           | AP          | 6502          | Open          |  
| 5         | VIP Parking Pass Not Valid  | HIG           | EU          | 8005          | Open          |  
| 8         | Invalid QR Code Scanned     | HIG           | NA          | 6100          | Resolved      |  

### Solution Query

```sql
SELECT
    ticket_id,
    ticket_title,
    LEFT(ticket_code,3) AS priority_code,
    RIGHT(LEFT(ticket_code,5),2) AS region_code,
    RIGHT(ticket_code,4) AS ticket_number,
    ticket_status
FROM event_tickets
WHERE RIGHT(ticket_code,4) > 6000 AND LEFT(ticket_code,3) = 'HIG';
```
