### Column Types in SQLite
- **INTEGER**: Whole numbers, 1-8 bytes.
- **REAL**: Floating-point numbers, 8 bytes.
- **TEXT**: UTF-8/16 text.
- **BLOB**: Binary data, stored as-is.
- **NUMERIC**: Converts values to INTEGER, REAL, or TEXT as needed.

SQLite uses **type affinity**, meaning columns prefer certain data types but can store any type.

### Column Constraints in SQLite
- **PRIMARY KEY**: Unique identifier for rows; auto-indexed.
- **UNIQUE**: Prevents duplicate values.
- **NOT NULL**: Disallows NULL values.
- **CHECK**: Enforces a condition, e.g., `CHECK(age >= 18)`.
- **DEFAULT**: Sets a default value when none is provided.

These constraints help maintain data integrity.

enforcing a UNIQUE column constraint can have performance considerations.
PRIMARY KEY implies the UNIQUE constraint
If a column is
marked both UNIQUE and PRIMARY KEY, only one index will be created.
PRIMARY KEY does not imply NOT NULL
mark at least one column from each PRIMARY KEY as NOT NULL.

## table constrains 

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username TEXT UNIQUE,
    email TEXT,
    age INTEGER CHECK (age >= 18),
    CONSTRAINT unique_email UNIQUE (email)
);
```

Explanation:
- `PRIMARY KEY` on `id` ensures each `id` is unique and automatically indexed.
- `UNIQUE` on `username` ensures no two users can have the same username.
- `CHECK (age >= 18)` ensures all users are at least 18.
- `UNIQUE` constraint on `email` (using `CONSTRAINT unique_email`) ensures each email is unique.


When a UNIQUE or PRIMARY KEY constraint is applied to multiple columns

```sql
CREATE TABLE rooms(
    room_number INTEGER NOT NULL ,
    building_number INTEGER NOT NULL,
    [...,]
    PRIMARY KEY( room_number, building_number )
);
```

SQLite supports a limited version of the ALTER TABLE command. Currently, there are
only two operations supported by ALTER TABLE: add column and rename. The add col-
umn variant allows you to add new columns to an existing table. It cannot remove
them. New columns are always added to the end of the column list. Several other
restrictions apply.