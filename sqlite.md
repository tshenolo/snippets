# SQLite Cheatsheet

This cheatsheet covers common `sqlite3` CLI commands and SQL syntax for SQLite.
SQLite is a serverless, self-contained, transactional SQL database engine. The database is typically a single file.

## `sqlite3` CLI Commands

The `sqlite3` command-line interface is used to interact with SQLite databases.

*   **Open or Create a database file**:
    ```bash
    sqlite3 mydatabase.db # Opens mydatabase.db, creates it if it doesn't exist
    ```
*   **In-memory database** (lost when session ends):
    ```bash
    sqlite3 :memory:
    ```
*   **Common dot-commands (executed within the `sqlite3` shell):**
    *   `.help`: Show help for dot-commands.
    *   `.open <filename.db>`: Close current database and open a new one.
    *   `.databases`: List attached database files and their names.
    *   `.tables`: List all tables in the current database.
    *   `.tables <pattern>`: List tables matching a LIKE pattern.
        ```sqlite
        .tables emp%
        ```
    *   `.schema <table_name>`: Show the `CREATE TABLE` statement for the specified table. If no table name, shows all schemas.
        ```sqlite
        .schema employees
        ```
    *   `.fullschema`: Show the entire schema, including system tables and indexes.
    *   `.indexes <table_name>`: List indexes for a table.
    *   `.headers on|off`: Turn display of column headers on or off.
        ```sqlite
        .headers on
        ```
    *   `.mode <mode_name>`: Set output mode. Common modes:
        *   `list` (default, values separated by a separator string)
        *   `csv` (Comma Separated Values)
        *   `column` (Left-aligned columns)
        *   `table` (ASCII-art table)
        *   `html` (HTML table)
        *   `json` (JSON output, SQLite 3.33.0+)
        ```sqlite
        .mode column
        .headers on
        ```
    *   `.separator <string>`: Change separator for `list` mode (default is `|`). For CSV, use `.mode csv`.
    *   `.width <num1> <num2> ...`: Set column widths for `column` mode. Negative values right-justify.
        ```sqlite
        .width 15 20 -10
        ```
    *   `.output <filename>`: Send output to a file instead of stdout.
        ```sqlite
        .output query_results.txt
        SELECT * FROM employees;
        .output stdout  -- Reset output to screen
        ```
    *   `.import <filename> <table_name>`: Import data from a file into a table. File format should match current `.mode` (e.g., CSV).
        ```sqlite
        .mode csv
        .import users_data.csv users
        ```
    *   `.dump`: Dump the entire database in SQL text format.
    *   `.dump <table_name>`: Dump a specific table in SQL text format.
        ```sqlite
        .output backup.sql
        .dump
        .output stdout
        ```
    *   `.read <filename.sql>`: Execute SQL commands from a file.
        ```sqlite
        .read setup_script.sql
        ```
    *   `.show`: Show current settings for various dot-commands (like `.mode`, `.headers`).
    *   `.timer on|off`: Turn CPU timer on or off for queries.
    *   `.quit` or `.exit`: Exit the `sqlite3` shell.
    *   `.shell <command>` or `.!<command>`: Run a shell command.

## SQL: Data Definition Language (DDL)

SQLite uses dynamic typing with "Type Affinity". You can store any value in almost any column, but it tries to coerce values to the declared type. Common affinities: `TEXT`, `NUMERIC`, `INTEGER`, `REAL`, `BLOB`.

*   **Create a table**:
    ```sql
    CREATE TABLE employees (
        id INTEGER PRIMARY KEY AUTOINCREMENT, -- Recommended for auto-incrementing PK
        first_name TEXT NOT NULL,
        last_name TEXT NOT NULL,
        email TEXT UNIQUE,
        hire_date TEXT, -- Often stored as TEXT in 'YYYY-MM-DD' format
        salary REAL,
        department_id INTEGER,
        FOREIGN KEY (department_id) REFERENCES departments(id)
    );

    CREATE TABLE departments (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL UNIQUE
    );
    ```
    *   `IF NOT EXISTS` can be used: `CREATE TABLE IF NOT EXISTS employees (...)`
*   **Data Type Affinities**:
    *   `TEXT`: Stores strings.
    *   `NUMERIC`: Stores numbers. Tries to store as INTEGER or REAL.
    *   `INTEGER`: Stores integers.
    *   `REAL`: Stores floating-point numbers.
    *   `BLOB`: Stores binary data as is.
    *   (No specific `BOOLEAN` or `DATE`/`TIME` types, typically use `INTEGER` (0/1) for boolean and `TEXT` or `INTEGER` (Unix epoch) for dates/times.)
*   **Constraints**:
    *   `PRIMARY KEY`: Uniquely identifies rows. `INTEGER PRIMARY KEY AUTOINCREMENT` is common.
    *   `FOREIGN KEY (...) REFERENCES ...`: Enforced if `PRAGMA foreign_keys = ON;`.
    *   `UNIQUE`: Values in the column must be distinct.
    *   `NOT NULL`: Column cannot contain NULL values.
    *   `DEFAULT <value>`: Default value for the column.
    *   `CHECK (<condition>)`: Value must satisfy the condition.
    *   `COLLATE <collation_name>`: Specify text collation (e.g., `NOCASE` for case-insensitive comparisons).
        ```sql
        CREATE TABLE products (name TEXT UNIQUE COLLATE NOCASE);
        ```
*   **Alter a table**: SQLite has limited `ALTER TABLE` support compared to other RDBMS.
    *   Rename a table:
        ```sql
        ALTER TABLE employees RENAME TO staff;
        ```
    *   Add a column:
        ```sql
        ALTER TABLE staff ADD COLUMN phone_number TEXT;
        ALTER TABLE staff ADD COLUMN status TEXT DEFAULT 'active' NOT NULL;
        ```
    *   Rename a column (SQLite 3.25.0+):
        ```sql
        ALTER TABLE staff RENAME COLUMN phone_number TO contact_phone;
        ```
    *   Drop a column (SQLite 3.35.0+):
        ```sql
        ALTER TABLE staff DROP COLUMN old_notes;
        ```
    *   *Note: Modifying or dropping constraints, or changing column types often requires a more complex process: create new table, copy data, drop old table, rename new table.*
*   **Drop a table**:
    ```sql
    DROP TABLE staff;
    DROP TABLE IF EXISTS staff;
    ```
*   **Create an index**:
    ```sql
    CREATE INDEX idx_staff_last_name ON staff (last_name);
    CREATE UNIQUE INDEX idx_staff_email ON staff (email);
    ```
*   **Drop an index**:
    ```sql
    DROP INDEX idx_staff_last_name;
    DROP INDEX IF EXISTS idx_staff_last_name;
    ```
*   **Create a view**:
    ```sql
    CREATE VIEW active_staff AS
    SELECT id, first_name, last_name, email
    FROM staff
    WHERE status = 'active';
    ```
*   **Drop a view**:
    ```sql
    DROP VIEW active_staff;
    ```

## SQL: Data Manipulation Language (DML)

*   **Insert data**:
    ```sql
    INSERT INTO departments (name) VALUES ('Technology');
    INSERT INTO departments (name) VALUES ('HR'), ('Finance');

    INSERT INTO staff (first_name, last_name, email, salary, department_id)
    VALUES ('Jane', 'Doe', 'jane.doe@example.com', 70000.0, 1);
    ```
    *   `INSERT OR IGNORE`: If a constraint (like UNIQUE) would be violated, the INSERT is ignored.
        ```sql
        INSERT OR IGNORE INTO staff (email, first_name, last_name) VALUES ('jane.doe@example.com', 'Janet', 'Doe');
        ```
    *   `INSERT OR REPLACE`: If a constraint (like UNIQUE on email) is violated, the existing row is deleted and the new row is inserted.
        ```sql
        INSERT OR REPLACE INTO staff (id, email, first_name, last_name) VALUES (1, 'jane.doe.new@example.com', 'Jane', 'Smith');
        ```
    *   `UPSERT` (SQLite 3.24.0+): `INSERT ... ON CONFLICT ... DO UPDATE ...`
        ```sql
        INSERT INTO staff (email, first_name, last_name, salary)
        VALUES ('john.ray@example.com', 'John', 'Ray', 55000.0)
        ON CONFLICT(email) DO UPDATE SET
            salary = excluded.salary + 5000, -- 'excluded' refers to values from the attempted INSERT
            last_name = excluded.last_name
        WHERE staff.salary < excluded.salary; -- Optional WHERE for the UPDATE
        ```
*   **Select data**:
    ```sql
    SELECT * FROM staff;
    SELECT first_name, last_name, salary FROM staff WHERE department_id = 1 ORDER BY last_name ASC LIMIT 10 OFFSET 0;
    SELECT DISTINCT department_id FROM staff;
    SELECT first_name || ' ' || last_name AS full_name FROM staff; -- String concatenation
    SELECT COUNT(*) AS total_staff FROM staff;
    SELECT department_id, AVG(salary) AS avg_salary FROM staff GROUP BY department_id HAVING AVG(salary) > 60000;
    ```
    *   **Operators**: Similar to other SQL dialects (`=`, `!=` or `<>`, `<`, `>`, `<=`, `>=`, `AND`, `OR`, `NOT`, `BETWEEN`, `LIKE`, `GLOB` (shell-like wildcards), `IN`, `IS NULL`, `IS NOT NULL`).
    *   **Date and Time Functions**: SQLite doesn't have native date/time types, but provides functions to work with TEXT, REAL, or INTEGER representations.
        *   `date('now')`, `time('now')`, `datetime('now')`
        *   `strftime('%Y-%m-%d', hire_date)`
        ```sql
        SELECT first_name, hire_date FROM staff WHERE date(hire_date) > date('now', '-1 year');
        ```
*   **Update data**:
    ```sql
    UPDATE staff
    SET salary = salary * 1.05, email = 'jane.d.new@example.com'
    WHERE id = 1;
    ```
    *   `UPDATE OR IGNORE`, `UPDATE OR REPLACE`, `UPDATE OR ROLLBACK`, `UPDATE OR ABORT`, `UPDATE OR FAIL` are possible for conflict resolution.
*   **Delete data**:
    ```sql
    DELETE FROM staff WHERE id = 5;
    -- DELETE FROM staff; -- Deletes all rows!
    ```
*   **Truncate table** (SQLite has no direct `TRUNCATE TABLE` command like other RDBMS. Use `DELETE` without a `WHERE` clause):
    ```sql
    DELETE FROM staff;
    VACUUM; -- To reclaim disk space and reset AUTOINCREMENT for the table (if applicable)
    -- Or to reset AUTOINCREMENT for a specific table:
    -- DELETE FROM sqlite_sequence WHERE name='staff';
    ```

## SQL: Transaction Control

SQLite transactions are ACID compliant. By default, each command outside an explicit transaction is its own transaction (autocommit behavior, though this is handled at a lower level).

*   **Begin a transaction**:
    ```sql
    BEGIN TRANSACTION;
    -- or just BEGIN;
    -- or BEGIN DEFERRED; (default)
    -- or BEGIN IMMEDIATE; (acquires write lock immediately)
    -- or BEGIN EXCLUSIVE; (acquires exclusive lock immediately)
    ```
*   **Commit a transaction**:
    ```sql
    COMMIT;
    -- or END TRANSACTION;
    ```
*   **Rollback a transaction**:
    ```sql
    ROLLBACK;
    -- or ROLLBACK TRANSACTION;
    ```
*   **Savepoints**:
    ```sql
    BEGIN;
    INSERT INTO staff (first_name) VALUES ('Temp');
    SAVEPOINT my_savepoint;
    UPDATE staff SET last_name = 'User' WHERE first_name = 'Temp';
    -- If error:
    -- ROLLBACK TO SAVEPOINT my_savepoint;
    RELEASE SAVEPOINT my_savepoint; -- Optional, commits changes since savepoint as part of larger transaction
    COMMIT;
    ```

## Pragmas

Special commands to modify SQLite operation or query internal data.

*   **Enable/Disable Foreign Key Constraints** (disabled by default for compatibility):
    ```sql
    PRAGMA foreign_keys = ON;
    PRAGMA foreign_keys = OFF;
    PRAGMA foreign_keys; -- Query current state
    ```
*   **Query database schema version**:
    ```sql
    PRAGMA schema_version;
    ```
*   **Force database integrity check**:
    ```sql
    PRAGMA integrity_check;
    ```
*   **Optimize database file**:
    ```sql
    PRAGMA optimize; -- SQLite 3.18.0+
    ```
*   **Rebuild database file** (reclaims unused space, defragments):
    ```sql
    VACUUM;
    ```
*   **Journal Mode** (controls how transactions are written):
    ```sql
    PRAGMA journal_mode; -- Query current mode (e.g., DELETE, TRUNCATE, PERSIST, WAL, MEMORY, OFF)
    PRAGMA journal_mode = WAL; -- Write-Ahead Logging, good for concurrency
    ```
*   **Synchronous Setting** (controls how aggressively SQLite writes to disk):
    ```sql
    PRAGMA synchronous; -- Query current (0=OFF, 1=NORMAL, 2=FULL (default), 3=EXTRA)
    PRAGMA synchronous = NORMAL;
    ```
*   **User Version** (application-defined database version):
    ```sql
    PRAGMA user_version;
    PRAGMA user_version = 2;
    ```
*   **List table information**:
    ```sql
    PRAGMA table_info(table_name);
    ```
*   **List index information**:
    ```sql
    PRAGMA index_list(table_name);
    PRAGMA index_info(index_name);
    ```

## Full-Text Search (FTS3/FTS4/FTS5)

SQLite supports full-text search via virtual table modules. FTS5 is the latest and recommended.

*   **Create an FTS5 virtual table**:
    ```sql
    CREATE VIRTUAL TABLE articles_fts USING fts5(title, body, content='articles', content_rowid='id');
    -- 'content' and 'content_rowid' link it to the 'articles' table for easier updates.
    ```
*   **Populate FTS table (if using 'content' option, often done with triggers)**:
    ```sql
    -- Example trigger to keep FTS table in sync
    CREATE TRIGGER articles_ai AFTER INSERT ON articles BEGIN
      INSERT INTO articles_fts (rowid, title, body) VALUES (new.id, new.title, new.body);
    END;
    CREATE TRIGGER articles_ad AFTER DELETE ON articles BEGIN
      DELETE FROM articles_fts WHERE rowid=old.id;
    END;
    CREATE TRIGGER articles_au AFTER UPDATE ON articles BEGIN
      UPDATE articles_fts SET title=new.title, body=new.body WHERE rowid=new.id;
    END;
    -- Initial population:
    -- INSERT INTO articles_fts (rowid, title, body) SELECT id, title, body FROM articles;
    ```
*   **Search the FTS table**:
    ```sql
    SELECT rowid, title, snippet(articles_fts, 0, '<b>', '</b>', '...', 15) as search_snippet
    FROM articles_fts
    WHERE articles_fts MATCH 'search query AND terms'
    ORDER BY rank; -- 'rank' is an auxiliary column provided by FTS
    ```
    *   FTS5 supports advanced queries (NEAR, PHRASE, boolean operators AND/OR/NOT).

This provides a good level of detail for `sqlite.md`. I'll continue with `ssh.md` next.The `sqlite.md` cheatsheet has been successfully updated with detailed `sqlite3` CLI commands, SQL examples (DDL, DML, TCL), and common PRAGMA statements, formatted as requested.

Next, I will enhance `ssh.md` with more specific command examples and explanations for various SSH functionalities.
