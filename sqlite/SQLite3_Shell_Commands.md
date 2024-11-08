# Useful SQLite3 Shell Commands

Here is a list of some of the most useful shell-specific commands in `sqlite3`:

Two of the more useful dot-commands (besides .help) are ***.headers*** and ***.mode***. Both of
these control some aspect of the database output. Turning headers on and setting the
output mode to column will produce a table that most people find easier to read:
```sql
sqlite> SELECT 'abc' AS start, 'xyz' AS end;
abc|xyz
sqlite> .headers on
sqlite> .mode column
sqlite> SELECT 'abc' AS start, 'xyz' AS end;
start      end
---------- ----------
abc         xyz
sqlite>
```


**`.read <file>`**  
Reads and executes SQL commands from a file. This is useful for running batch scripts.
```sh
.read script.sql
```

**`.open <database>`**  
   Opens a SQLite database file. If the file doesn’t exist, it is created.
   ```sh
   .open mydatabase.db
   ```

**`.tables`**  
   Lists all the tables in the currently opened database.
   ```sh
   .tables
   ```

**`.schema <table>`**  
   Shows the schema (structure) of a specific table or all tables if no table name is provided.
   ```sh
   .schema mytable
   ```

**`.help`**  
   Displays a list of all available shell commands and their descriptions.
   ```sh
   .help
   ```


**`.mode <mode>`**  
   Sets the output mode (e.g., `csv`, `column`, `list`, `table`, etc.) for query results.
   ```sh
   .mode column
   .mode csv
   ```

**`.headers <on|off>`**  
   Toggles the display of column headers in query results.
   ```sh
   .headers on
   .headers off
   ```

**`.import <file> <table>`**  
   Imports data from a CSV file into the specified table.
   ```sh
   .import data.csv mytable
   ```

**`.dump`**  
    Dumps the entire database (or a specific table) as SQL statements that can be used to recreate the database.
    ```sh
    .dump
    .dump mytable
    ```

**`.transaction`**  
    Begins a new transaction. Useful for batch updates.
    ```sh
    .transaction
    ```

**`.clone <database>`**  
    Creates a copy of the current database in the specified file.
    ```sh
    .clone mybackup.db
    ```

**`.stats`**  
    Displays statistics about the current database, including the size of tables and indexes.
    ```sh
    .stats
    ```

**`.exit` or `.quit`**  
    Exits the SQLite shell.

