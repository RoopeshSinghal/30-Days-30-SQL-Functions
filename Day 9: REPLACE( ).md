## Day 9: REPLACE() 

The SQL `REPLACE()` function is used to search for a specified substring within a string and replace it with another substring. This is particularly useful for cleaning or modifying data when certain patterns or characters need to be updated.

### Syntax:

```sql
SELECT REPLACE(string, from_string, new_string) ; 
```

• string: The original string.
<br>• from_substring: The substring to be replaced.
<br>• to_substring: The substring to replace with.

### Example:

The following example demonstrates how to replace underscores (`_`) with spaces (` `) in product names.

```sql
SELECT REPLACE('Smartphone_Pro_Max', '_', ' ') AS UpdatedName;
```

| UpdatedName        |
|--------------------|
| Smartphone Pro Max |

### Question:


### Problem Statement

You are working with a `customers` table that contains the following columns:  

| Column Name       | Data Type     | Description                                         |  
|-------------------|---------------|-----------------------------------------------------|  
| `customer_id`     | INT           | Unique ID for each customer                         |  
| `email_address`   | VARCHAR(100)  | Email addresses that may contain invalid characters |  
| `phone_number`    | VARCHAR(15)   | Customer's phone number                             |  

The `email_address` column contains email addresses where some invalid characters
(like `#` and `%`) are mistakenly used in place of `@` or `_` (e.g., `john#doe%gmail.com`).  

Task:
Write a query to clean the `email_address` column by:  
1. Replacing the `#` character with `_`.
2. Replacing the `%` character with `@`.
3. Display the cleaned email addresses along with `customer_id`.

### Schema setup

```sql
CREATE TABLE customers (
    customer_id INT,
    email_address VARCHAR(100),
    phone_number VARCHAR(15)
);

INSERT INTO customers (customer_id, email_address, phone_number) VALUES
(1, 'john#doe%gmail.com', '1234567890'),
(2, 'jane#doe%yahoo.com', '9876543210'),
(3, 'mark#smith%hotmail.com', '5556667777'),
(4, 'alice#brown%outlook.com', '4445556666'),
(5, 'bob#white%icloud.com', '1112223333'),
(6, 'emma#jones%company.com', '7778889999'),
(7, 'lucas#johnson%business.org', '9998887777'),
(8, 'mia#lee%university.edu', '6665554444');
```

### Expected output

| customer_id | cleaned_email_address       |
|-------------|-----------------------------|
| 1           | john_doe@gmail.com          |
| 2           | jane_doe@yahoo.com          |
| 3           | mark_smith@hotmail.com      |
| 4           | alice_brown@outlook.com     |
| 5           | bob_white@icloud.com        |
| 6           | emma_jones@company.com      |
| 7           | lucas_johnson@business.org  |
| 8           | mia_lee@university.edu      |

### Solution Query

```sql
SELECT
    customer_id,
    REPLACE(REPLACE(email_address,'%','@'),'#','_') AS cleaned_email_address
FROM customers;
```
