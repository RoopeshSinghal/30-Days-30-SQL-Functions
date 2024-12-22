## Day 11: CHAR_LENGTH()

The SQL CHAR_LENGTH() function returns the number of characters in a given string. This function counts every character, including spaces, special characters, and punctuation marks. It is useful for validating input lengths, analyzing string data, or performing quality checks on text fields.

### Syntax:

```sql
SELECT CHAR_LENGTH(string) ; 
```

• string: The input string whose length is to be determined.

### Example:

The following example demonstrates how to calculate the length of a customer's name.

```sql
SELECT 
 'John Doe' AS Name, 
 CHAR_LENGTH('John Doe') AS NameLength;
```

| Name     | NameLength | 
|----------|------------|
| John Doe |   8        | 

### Question:

### Problem Statement

You are managing a system that tracks customer support tickets. The ticket details are stored in the `support_tickets` table,
which has the following schema:

| Column Name    | Data Type     | Description                         |  
|----------------|---------------|-------------------------------------|  
| ticket_id      | INT           | Unique ID for each support ticket   |  
| ticket_title   | VARCHAR(255)  | Title of the support ticket         |  
| ticket_status  | VARCHAR(20)   | Status of the ticket                |  
| ticket_details | TEXT          | Detailed description of the ticket  |  

Task:  
1. Identify tickets where:  
   a. The title exceeds 40 characters.  
   b. The total length of the title and status combined exceeds 100 characters.  
2. Display the ticket_id, ticket_title, ticket_status, and their combined length.  
3. Additionally, include a calculated column to flag such tickets as "Needs Review" .  
   
### Schema setup

```sql
CREATE TABLE support_tickets (
    ticket_id INT,
    ticket_title VARCHAR(255),
    ticket_status VARCHAR(20),
    ticket_details TEXT
);

INSERT INTO support_tickets (ticket_id, ticket_title, ticket_status, ticket_details) VALUES
(1, 'Unable to access account due to password reset failure', 'Open', 'Customer reports that they cannot reset their password.'),
(2, 'Error 404 encountered on product page', 'Closed', 'Customer could not find the product page and encountered a 404 error.'),
(3, 'Request for refund due to damaged item received', 'Pending', 'Customer has received a damaged item and is requesting a refund.'),
(4, 'Delayed shipping for order #12345', 'Open', 'Customer reports that their order has not been shipped yet.'),
(5, 'Account suspended after multiple login attempts', 'Resolved', 'Customer account was suspended after failed login attempts. Needs review.'),
(6, 'Feature request: Add dark mode to the app', 'Open', 'Customer requests adding a dark mode feature to improve usability.'),
(7, 'Missing invoice for order placed on December 1', 'Closed', 'Customer did not receive an invoice for their recent order.'),
(8, 'Complaint about poor customer service experience', 'Pending', 'Customer reports an unsatisfactory experience with customer service.');
```

### Expected output

| ticket_id | ticket_title                                            | ticket_status | combined_length | review_status |
|-----------|---------------------------------------------------------|---------------|-----------------|---------------|
| 1         | Unable to access account due to password reset failure | Open          | 58              | Needs Review  |
| 3         | Request for refund due to damaged item received        | Pending       | 54              | Needs Review  |
| 5         | Account suspended after multiple login attempts        | Resolved      | 55              | Needs Review  |
| 6         | Feature request: Add dark mode to the app              | Open          | 45              | Needs Review  |
| 7         | Missing invoice for order placed on December 1         | Closed        | 52              | Needs Review  |
| 8         | Complaint about poor customer service experience       | Pending       | 55              | Needs Review  |

### Solution Query

```sql
SELECT 
    ticket_id,
    ticket_title,
    ticket_status,
    CHAR_LENGTH(ticket_title) + CHAR_LENGTH(ticket_status) AS combined_length,
    CASE 
        WHEN CHAR_LENGTH(ticket_title) > 40 OR 
             (CHAR_LENGTH(ticket_title) + CHAR_LENGTH(ticket_status)) > 100 THEN 'Needs Review'
        ELSE 'OK'
    END AS review_status
FROM support_tickets
WHERE CHAR_LENGTH(ticket_title) > 40
   OR (CHAR_LENGTH(ticket_title) + CHAR_LENGTH(ticket_status)) > 100;
```
