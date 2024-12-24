## Day 15: REGEXP AND NOT REGEXP

The SQL REGEXP function allows you to perform pattern matching using regular expressions. It is useful for finding strings that match complex patterns, validating formats, or extracting specific substrings.
<br>The SQL NOT REGEXP function filters data by excluding strings that match a specific regular expression pattern. This is useful for data validation and cleaning, allowing you to identify and remove entries that don't conform to expected formats. For example, you could use it to find invalid email addresses or phone numbers in a database.

### Syntax:

```sql
SELECT column_name 
FROM table_name 
WHERE column_name REGEXP / NOT REGEXP 'pattern'; 
```

### Examples:

The following example demonstrates how to find users whose email ends with .com.

```sql
SELECT * 
FROM users 
WHERE email REGEXP '\\.com$'; 
```

| user_id | username   | email                |
|---------|------------|----------------------|
| 1       | alice123   | alice@example.in     |
| 4       | david_john | david.john@xyz.in    |

The following example demonstrates how to find users whose email not ends with .com.

```sql
SELECT * 
FROM users 
WHERE email NOT REGEXP '\\.com$'; 
```

| user_id | username   | email                |
|---------|------------|----------------------|
| 1       | alice123   | alice@example.in     |
| 4       | david_john | david.john@xyz.in    |

### Question:

### Problem Statement

ou are managing a user accounts database for a platform that enforces strict username and email validation. The `users` table has the following schema:  

| Column Name  | Data Type     | Description                             |  
|--------------|---------------|-----------------------------------------|  
| user_id      | INT           | Unique ID for each user                 |  
| username     | VARCHAR(50)   | The username chosen by the user         |  
| email        | VARCHAR(100)  | The user's email address                |  
| created_at   | DATE          | The date when the account was created   |  

Task:  

1. Extract Valid Usernames:  
   • A valid username contains only alphanumeric characters and underscores (`_`) but cannot start or end with an underscore.  
2. Validate Emails:  
   • The email must follow the format: `text@domain.extension` where:  
     • `text` can include alphanumeric characters and periods (`.`).  
     • `domain` must contain only alphanumeric characters.  
     • `extension` is between 2 to 4 alphabetic characters.  
3. Find and Display:  
   • Users with invalid usernames or invalid emails.  

   
### Schema setup

```sql
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    username VARCHAR(50),
    email VARCHAR(100),
    created_at DATE
);

INSERT INTO users (user_id, username, email, created_at) VALUES
(1, 'john_doe', 'john.doe@gmail.com', '2023-12-01'),
(2, 'alice123', 'alice@company.net', '2023-11-20'),
(3, '_carol', 'carol@domain.org', '2023-10-15'),
(4, 'bob_smith', 'bob.smith@gmail.com', '2023-09-10'),
(5, 'eve.2024', 'eve@example', '2023-08-25'),
(6, '_invalid_', 'invalid.email@domain.com', '2023-07-18'),
(7, 'michael', 'michael@service.co', '2023-06-14');
```

### Expected output

| user_id | username     | email                     | error_reason                |  
|---------|--------------|---------------------------|-----------------------------|  
| 3       | _carol       | carol@domain.org          | Invalid username            |  
| 5       | eve.2024     | eve@example               | Invalid email               |  
| 6       | _invalid_    | invalid.email@domain.com  | Invalid username and email  |  

### Solution Query

```sql
SELECT 
    user_id,
    username,
    email,
    CASE
        WHEN username NOT REGEXP '^[A-Za-z0-9]+(_[A-Za-z0-9]+)*$' AND 
             email NOT REGEXP '^[A-Za-z0-9.]+@[A-Za-z0-9]+\\.[A-Za-z]{2,4}$'
             THEN 'Invalid username and email'
        WHEN username NOT REGEXP '^[A-Za-z0-9]+(_[A-Za-z0-9]+)*$' 
             THEN 'Invalid username'
        WHEN email NOT REGEXP '^[A-Za-z0-9.]+@[A-Za-z0-9]+\\.[A-Za-z]{2,4}$'
             THEN 'Invalid email'
        ELSE NULL
    END AS error_reason
FROM users
WHERE 
    username NOT REGEXP '^[A-Za-z0-9]+(_[A-Za-z0-9]+)*$'
    OR email NOT REGEXP '^[A-Za-z0-9.]+@[A-Za-z0-9]+\\.[A-Za-z]{2,4}$';
```
