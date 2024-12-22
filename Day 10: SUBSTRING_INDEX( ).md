## Day 10: SUBSTRING_INDEX()

The SQL `SUBSTRING_INDEX()` function extracts a substring from a string based on a specified delimiter and occurrence count. This is particularly useful for splitting strings or extracting meaningful portions of data from structured text fields. 

### Syntax:

```sql
SELECT SUBSTRING_INDEX( str, delim, count ) ; 
```

• str : The original string from which we want to create a substring.
<br>• delim : Is a string that acts as a delimiter. The function performs a case-sensitive match when searching for the delimiter.
<br>• count : It identifies the number of times to search for the delimiter. It can be both a positive or negative number. If it is a positive number, this function returns all to the left of the delimiter. If it is a negative number, this function returns all to the right of the delimiter.


### Example:

The following example demonstrates how to extract the first and last parts of a customer's full name.

```sql
SELECT 
 SUBSTRING_INDEX('John Doe Smith', ' ', 1) AS FirstName, 
 SUBSTRING_INDEX('John Doe Smith', ' ', -1) AS LastName;
```

| FirstName | LastName | 
|-----------|----------|
| John      |    Smith | 

### Question:


### Problem Statement

The `customers` table stores customers' full names in the `full_name` column,where names are stored
in the format `First Middle Last`.  

Write a query to:  
1. Extract only the first name from the `full_name` column.  
2. Extract only the last name from the `full_name` column.  
3. Extract the domain of the email address (everything after the `@`).  

| Column Name       | Data Type     | Description                                         |  
|-------------------|---------------|-----------------------------------------------------|  
| `customer_id`     | INT           | Unique ID for each customer                         |  
| `full_name`       | VARCHAR(15)   | Customer's Name                                     |  
| `email_address`   | VARCHAR(100)  | Customer's Email Address                            |  

### Schema setup

```sql
CREATE TABLE customers (
    customer_id INT,
    full_name VARCHAR(20),
    email_address VARCHAR(30)
);

INSERT INTO customers (customer_id, full_name, email_address) VALUES
(1, 'John Doe Smith', 'john.doe.smith@gmail.com'),
(2, 'Jane Alice Brown', 'jane.brown@hotmail.com'),
(3, 'Mark Alan Lee', 'mark.lee@yahoo.com'),
(4, 'Alice Carol White', 'alice.white@outlook.com'),
(5, 'Bob Charlie Davis', 'bob.davis@icloud.com'),
(6, 'Emma Grace Taylor', 'emma.taylor@company.com'),
(7, 'Lucas Henry Johnson', 'lucas.johnson@business.org'),
(8, 'Mia Sophia Green', 'mia.green@university.edu');
```

### Expected output

| customer_id | first_name | last_name | email_domain       |  
|-------------|------------|-----------|--------------------|  
| 1           | John       | Smith     | gmail.com          |  
| 2           | Jane       | Brown     | hotmail.com        |  
| 3           | Mark       | Lee       | yahoo.com          |  
| 4           | Alice      | White     | outlook.com        |  
| 5           | Bob        | Davis     | icloud.com         |  
| 6           | Emma       | Taylor    | company.com        |  
| 7           | Lucas      | Johnson   | business.org       |  
| 8           | Mia        | Green     | university.edu     |  

### Solution Query

```sql
SELECT 
    customer_id,
    SUBSTRING_INDEX(full_name, ' ', 1) AS first_name,
    SUBSTRING_INDEX(full_name, ' ', -1) AS last_name,
    SUBSTRING_INDEX(email_address, '@', -1) AS email_domain
FROM customers;
```
