
# Useful SQLite3 Shell Commands

Here is a list of some of the most useful shell-specific commands in `sqlite3`:

1. **`.open <database>`**  
   Opens a SQLite database file. If the file doesn’t exist, it is created.
   ```sh
   .open mydatabase.db
   ```

2. **`.tables`**  
   Lists all the tables in the currently opened database.
   ```sh
   .tables
   ```

3. **`.schema <table>`**  
   Shows the schema (structure) of a specific table or all tables if no table name is provided.
   ```sh
   .schema mytable
   ```

4. **`.help`**  
   Displays a list of all available shell commands and their descriptions.
   ```sh
   .help
   ```

5. **`.exit`**  
   Exits the SQLite shell.
   ```sh
   .exit
   ```

6. **`.quit`**  
   Another way to exit the SQLite shell (same as `.exit`).
   ```sh
   .quit
   ```

7. **`.mode <mode>`**  
   Sets the output mode (e.g., `csv`, `column`, `list`, `table`, etc.) for query results.
   ```sh
   .mode column
   .mode csv
   ```

8. **`.headers <on|off>`**  
   Toggles the display of column headers in query results.
   ```sh
   .headers on
   .headers off
   ```

9. **`.import <file> <table>`**  
   Imports data from a CSV file into the specified table.
   ```sh
   .import data.csv mytable
   ```

10. **`.dump`**  
    Dumps the entire database (or a specific table) as SQL statements that can be used to recreate the database.
    ```sh
    .dump
    .dump mytable
    ```

11. **`.transaction`**  
    Begins a new transaction. Useful for batch updates.
    ```sh
    .transaction
    ```

12. **`.clone <database>`**  
    Creates a copy of the current database in the specified file.
    ```sh
    .clone mybackup.db
    ```

13. **`.stats`**  
    Displays statistics about the current database, including the size of tables and indexes.
    ```sh
    .stats
    ```

14. **`.exit` or `.quit`**  
    Exits the SQLite shell.
