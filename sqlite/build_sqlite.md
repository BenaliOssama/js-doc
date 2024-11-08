# Building sqlite

## The SQLite project consists of four major products:

### SQLite core
The SQLite core contains the actual database engine and public API. The core
can be built into a static or dynamic library, or it can be built in directly to an
application.

### sqlite3 command-line tool
The sqlite3 application is a command-line tool that is built on top of the SQLite
core. It allows a developer to issue interactive SQL commands to the SQLite core.
It is extremely useful for developing and debugging queries.

### Tcl extension
SQLite has a strong history with the Tcl language. This library is essentially a copy
of the SQLite core with the Tcl bindings tacked on. When compiled into a library,
this code exposes the SQLite interfaces to the Tcl language through the Tcl Exten-
sion Architecture (TEA). Outside of the native C API, these Tcl bindings are the
only official programming interface supported directly by the SQLite team.

### 17SQLite analyzer tool
The SQLite analyzer is used to analyze database files. It displays statistics about
the database file size, fragmentation, available free space, and other data points. It
is most useful for debugging performance issues related to the physical layout of
the database file. It can also be used to determine if it is appropriate to VACUUM
(repack and defragment) the database or not. The SQLite website provides pre-
compiled sqlite3_analyzer executables for most desktop platforms. The source
for the analyzer is only available through the development source distribution.

### mattn/go-sqlite3 
SQLite Core: This is the main SQLite library, written in C, which performs all database operations. The Go SQLite driver (mattn/go-sqlite3) uses the SQLite core, often via the Amalgamation (sqlite3.c), embedding it within the driver to execute SQL commands directly in Go applications.

**Step 1:** Go calls sql.Open("sqlite3", "data.db") → mattn/go-sqlite3 uses CGO to call sqlite3_open from sqlite3.c.
**Step 2:** Go executes a query with db.Query("SELECT * FROM users") → mattn/go-sqlite3 uses CGO to call the appropriate C function in sqlite3.c for executing SQL statements.
**Step 3:** SQLite Core processes the SQL, retrieves data, and CGO transfers this data back to Go in a structured format.