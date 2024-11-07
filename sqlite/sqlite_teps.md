# Key Database Concepts

## Relational vs Non-Relational Databases

### Relational Databases (SQL)
- Store data in structured tables with rows and columns.
- Use **SQL** for querying.
- Data is highly structured with relationships (e.g., foreign keys between tables).
- Example: **MySQL**, **PostgreSQL**.

### Non-Relational Databases (NoSQL)
- Store data in flexible formats like documents, key-value pairs, or graphs.
- Do not use fixed schemas, allowing greater flexibility.
- Example: **MongoDB** (document-based), **Redis** (key-value store).

**Key Difference:**
- Relational databases have structured tables and relationships, while non-relational databases offer more flexibility and schema-less designs.

---

## Non-Relational Database Features
- **No Joins:** Non-relational databases typically do not support joins. Data is often denormalized and stored together.
- **Common Uses:**
  - Real-time data (e.g., social media feeds).
  - Big data applications (e.g., IoT, analytics).
  - Content management systems (CMS).
  - E-commerce (product catalogs with varying attributes).
  - Gaming and session storage.

---

## SQLite and Images
- SQLite can store images as **BLOBs** (Binary Large Objects), but it is not ideal for large or numerous images.
- **Recommendation:** Store images as files in the filesystem and save only their paths in SQLite for better performance.

---

## ACID Properties
ACID-compliant databases ensure reliable and consistent transactions. They follow four key properties:

1. **Atomicity:** Transactions are all-or-nothing. Either all operations succeed, or none do.
2. **Consistency:** Transactions bring the database from one valid state to another.
3. **Isolation:** Transactions do not interfere with each other; each runs as if it’s the only transaction.
4. **Durability:** Once a transaction is committed, it is permanent, even in case of failures.

---

## Key Terms

- **Atomic:** Transactions are indivisible; they succeed or fail entirely.
- **Isolation:** Ensures that concurrent transactions do not interfere with each other.

---

This summarizes key database concepts, helping to distinguish relational vs non-relational databases, and explain how ACID properties ensure data integrity.


# SQLite and Concurrency in Go

## 1. SQLite and Concurrency
SQLite transactions are fully ACID-compliant
SQLite is a serverless, self-contained database engine that allows concurrent **read** access from multiple connections, but **write** access is limited to one connection at a time. To handle concurrency with multiple goroutines in Go, special care should be taken to avoid conflicts and ensure data integrity.

### 1.1. Atomicity and Isolation in Transactions
- **Atomicity**: Ensures that a transaction is either fully completed or fully rolled back (all-or-nothing).
- **Isolation**: Ensures that concurrent transactions do not interfere with each other. Each transaction is executed as if it's the only one.

## 2. Methods to Handle SQLite Concurrency in Go

### 2.1. Using Mutexes to Serialize Writes
To prevent multiple goroutines from writing to the database at the same time, use a **mutex** to serialize access.

#### Example:
```go
var mu sync.Mutex

func writeToDB(db *sql.DB, data string) {
	mu.Lock()
	defer mu.Unlock()

	// Perform database write operation
	_, err := db.Exec("INSERT INTO data (info) VALUES (?)", data)
	if err != nil {
		log.Fatal(err)
	}
}
# Using Transactions to Ensure Consistency

Transactions allow you to group multiple operations together to ensure atomicity, consistency, isolation, and durability (ACID properties). This ensures that either all operations in the transaction succeed, or none of them do (in case of an error).

## Code Explanation

The following Go code demonstrates how to use transactions with SQLite to ensure that multiple database operations are executed atomically.

```go
package main

import (
	"database/sql"
	"fmt"
	"log"
	_ "github.com/mattn/go-sqlite3"
)

func writeWithTransaction(db *sql.DB, data string) {
	// Start a new transaction
	tx, err := db.Begin() 
	if err != nil {
		log.Fatal(err)
	}

	// Example write operation within a transaction
	_, err = tx.Exec("INSERT INTO data (info) VALUES (?)", data)
	if err != nil {
		// Rollback transaction if an error occurs
		tx.Rollback() 
		log.Fatal(err)
	}

	// Commit the transaction if no errors
	err = tx.Commit() 
	if err != nil {
		log.Fatal(err)
	}
}
```

