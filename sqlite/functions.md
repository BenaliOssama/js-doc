In SQLite, a *function* is a built-in or user-defined operation that performs a specific calculation or transformation on values in SQL queries. Functions can be used in various parts of SQL statements, such as `SELECT`, `WHERE`, and `ORDER BY` clauses.

### Types of Functions in SQLite

1. **Aggregate Functions**: These perform calculations on multiple rows and return a single result, commonly used in conjunction with `GROUP BY`. Examples:
   - `COUNT(column_name)`: Counts the number of rows.
   - `SUM(column_name)`: Calculates the sum of values in a column.
   - `AVG(column_name)`: Finds the average of a column.
   - `MAX(column_name)`, `MIN(column_name)`: Find the maximum or minimum values in a column.

   ```sql
   SELECT AVG(price) FROM products;
   ```

2. **Scalar Functions**: These operate on individual values and return a single result for each input row. Examples include:
   - `UPPER(text)`, `LOWER(text)`: Change text to uppercase or lowercase.
   - `LENGTH(text)`: Returns the length of a text string.
   - `ROUND(number, decimals)`: Rounds a number to the specified decimal places.
   - `ABS(number)`: Returns the absolute value of a number.
   - `DATE('now')`, `DATETIME('now')`: Get the current date and time.

   ```sql
   SELECT UPPER(name) FROM users;
   ```

3. **Date and Time Functions**: SQLite provides various functions to work with dates and times, such as `DATE()`, `TIME()`, and `DATETIME()`, which allow for operations like adding/subtracting days or extracting parts of dates.

   ```sql
   SELECT DATE('now', '+7 days');  -- Returns the date 7 days from today
   ```

4. **User-Defined Functions**: SQLite also supports adding custom functions (typically in applications using SQLite), where users can define their own logic.

### Using Functions in Expressions

You can combine functions with expressions and conditions, like this:

```sql
SELECT name, ROUND(price * 1.1, 2) AS final_price FROM products WHERE LENGTH(name) > 5;
```

This example calculates a new price with a 10% increase (`ROUND(price * 1.1, 2)`) and only returns products with names longer than 5 characters.