## Day 16: GROUP_CONCAT()

The SQL `GROUP_CONCAT()` function concatenates values from a group into a single string, separated by a specified delimiter. It is useful for combining rows of data into a single row. 

### Syntax:

```sql
SELECT GROUP_CONCAT(column_name SEPARATOR 'delimiter') 
FROM table_name 
GROUP BY group_column; 
```

### Example:

The following example demonstrates how to list products purchased by each customer.

'Orders table' 
| order_id | customer_name | product_name     |  
|----------|---------------|------------------|  
| 1        | John Doe      | Laptop           |  
| 2        | John Doe      | Mouse            |  
| 3        | Jane Smith    | Keyboard         |  
| 4        | John Doe      | Monitor          |  
| 5        | Jane Smith    | USB Drive        |  

```sql
SELECT customer_name, GROUP_CONCAT(product_name SEPARATOR ', ') AS products 
FROM orders 
GROUP BY customer_name; 
```

This SQL query retrieves a list of customers and the products they have ordered, concatenated into a single string with a delimeter ','.

Output:  
| customer_name | products                 |  
|---------------|--------------------------|  
| John Doe      | Laptop, Mouse, Monitor   |  
| Jane Smith    | Keyboard, USB Drive      |  

### Question:

### Problem Statement

You are managing a university database containing information about students and the courses they are enrolled in. The `enrollments` table has the following schema:  

| Column Name  | Data Type     | Description                   |  
|--------------|---------------|-------------------------------|  
| student_id   | INT           | Unique ID for each student    |  
| student_name | VARCHAR(100)  | Full name of the student      |  
| course_id    | INT           | Unique ID for each course     |  
| course_name  | VARCHAR(100)  | Name of the course            |  

Task:  
1. For each student, list all the courses they are enrolled in, separated by a semicolon (`;`).  
2. Display only students who are enrolled in three or more courses.  
3. The result should include:  
   - `student_name`  
   - `courses_list` (a semicolon-separated list of course names)  
   - `total_courses`  
   
### Schema setup

```sql
CREATE TABLE enrollments (
    student_id INT,
    student_name VARCHAR(100),
    course_id INT,
    course_name VARCHAR(100)
);

INSERT INTO enrollments (student_id, student_name, course_id, course_name) VALUES
(1, 'Alice Johnson', 101, 'Math 101'),
(1, 'Alice Johnson', 102, 'Physics 102'),
(1, 'Alice Johnson', 103, 'Chemistry 103'),
(2, 'Bob Smith', 104, 'English 104'),
(2, 'Bob Smith', 105, 'History 105'),
(2, 'Bob Smith', 106, 'Art 106'),
(2, 'Bob Smith', 107, 'Math 101'),
(3, 'Charlie Brown', 108, 'Biology 107'),
(3, 'Charlie Brown', 109, 'Computer Science 108'),
(4, 'Diana Prince', 110, 'Psychology 109');
```

### Expected output

| student_name   | courses_list                                | total_courses |  
|----------------|---------------------------------------------|---------------|  
| Alice Johnson  | Math 101; Physics 102; Chemistry 103        | 3             |  
| Bob Smith      | English 104; History 105; Art 106; Math 101 | 4             |  

### Solution Query

```sql
Will be Added Tomorrow
```
