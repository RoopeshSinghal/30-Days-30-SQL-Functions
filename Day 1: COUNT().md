## Day 1: COUNT()

The SQL `COUNT()` function returns the number of records returned by a query. It is often used to count rows or specific values within a dataset.

### Syntax:
```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

### Example:
Count all employees in the Sales department

```sql
SELECT COUNT(*) 
FROM employees 
WHERE department = 'Sales';
```

### Question:
How would you count the number of employees who are not in the "Marketing" department?

```sql
SELECT COUNT(*)
FROM employees
WHERE department != 'Marketing';
```
