- SQLite is designed to be integrated directly into an executable.
- SQLite’s small code size and conservative resource use makes it well suited for
embedded systems running limited operating systems.
- SQLite uses a dynamic-type system for tables
- SQLite has the ability to create fully in-memory databases
- SQLite
depends on filesystem permissions to control access to the raw database file.
- Integer have a range of −9,223,372,036,854,775,808 to +9,223,372,
036,854,775,807, or roughly 19 digits
- Bulk inserts can be sped up by wrapping large groups of INSERT com-
mands inside a transaction.
- If no WHERE condition is given, the UPDATE command will attempt to up-
date the designated columns in every row of a table.
- If no WHERE condition is given, the DELETE command will attempt to delete
every row of a table.
- The rows of an SQL table have no defined order.
### Column Qualification
 When filtering or selecting, refer to column names in this format:
```sql
[[database_name.]table_name.]column_name
```
- You cannot use the equality operator (=) to test for NULLs. You must
use the IS NULL operator.
# Not the Best Choice in 

- High Transaction Rates
SQLite is able to support moderate transaction rates, but it is not designed to sup-
port the level of concurrent access provided by many client/server RDBMS prod-
ucts
- SQLite is specifically designed without a network component, and is best used as
a local resource
## The files data.db-shm and data.db-wal 

are temporary files created by SQLite when it operates in WAL (Write-Ahead Logging) mode:

### data.db-wal: The Write-Ahead Log file, where SQLite stores changes before writing them to the main database. This allows faster write operations and improves concurrency.

### data.db-shm: The Shared Memory file, used to coordinate access to the WAL file across multiple connections.

These files help manage efficient reads and writes in WAL mode and are deleted automatically when the database is closed properly.

### tool for analysing and getting some info
```bash
sqlite-analyzer mydatabase.db | grep -E "table|index|page"
```
```url
https://www.geeksforgeeks.org/introduction-of-relational-algebra-in-dbms/
```

**Three-Valued Logic (3VL)** in SQL is a system where expressions can result in three possible values: **TRUE**, **FALSE**, or **NULL** (UNKNOWN). This third value, `NULL`, represents missing or undefined data. 

In 3VL:

- **TRUE AND UNKNOWN** → UNKNOWN
- **FALSE OR UNKNOWN** → UNKNOWN
- **NOT UNKNOWN** → UNKNOWN

3VL helps SQL handle operations involving NULLs, ensuring that queries yield accurate results even with incomplete data.
you can create a view using the CREATE VIEW statement. A view is essentially a saved query that you can treat like a table for easier data access. Here’s the basic syntax:

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```