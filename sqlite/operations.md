## Simple Operators in SQLite

- **Unary Operators**:  
  - `+` and `-`: Adjust sign; `-` negates a value, `+` is a no-op.
  - `~`: Bitwise inversion (non-standard SQL).
  - `NOT`: Reverses Boolean logic using three-valued logic (3VL).

- **Binary Operators** (in descending precedence):
  - `||`: String concatenation (SQL standard).
  - `+`, `-`, `*`, `/`, `%`: Basic arithmetic (add, subtract, multiply, divide, modulus).
  - `|`, `&`, `<<`, `>>`: Bitwise OR, AND, left-shift, right-shift (non-standard SQL).
  - `<`, `<=`, `=>`, `>`: Comparison operators (3VL applies).
  - `=`, `==`, `!=`, `<>`: Equality/inequality tests (3VL applies).
  - `IN`, `LIKE`, `GLOB`, `MATCH`, `REGEXP`: Logical pattern matching.
  - `AND`, `OR`: Logical operators, subject to 3VL.

These operators enable various expressions and conditions in SQL queries.

## SQL commands are grouped into four main categories:

1. **Data Definition Language (DDL)**: Defines the structure of database objects (tables, views, indexes). Examples: `CREATE TABLE`, `DROP VIEW`.

2. **Data Manipulation Language (DML)**: Handles the actual data within tables, including inserting, updating, deleting, and querying data. Examples: `INSERT`, `SELECT`.

3. **Transaction Control Language (TCL)**: Manages transactions for DML and DDL commands. Examples: `BEGIN`, `COMMIT`.

4. **Data Control Language (DCL)**: Manages permissions and access control to the database. Examples: `GRANT`, `REVOKE`. SQLite does not support DCL as it lacks user management and permissions.

SQLite supports DDL, DML, and TCL but does not have DCL due to its simple permission model.