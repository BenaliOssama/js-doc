- SQLite is designed to be integrated directly into an executable.
- SQLite’s small code size and conservative resource use makes it well suited for
embedded systems running limited operating systems.
- SQLite uses a dynamic-type system for tables
- SQLite has the ability to create fully in-memory databases
- SQLite
depends on filesystem permissions to control access to the raw database file.
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
