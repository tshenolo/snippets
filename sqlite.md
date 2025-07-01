# SQLite Cheatsheet

*   **Characteristics**: Serverless, self-contained, zero-configuration, transactional SQL database engine. Database is a single file.
*   **`sqlite3` CLI**: `.open filename.db`, `.tables`, `.schema tablename`, `.quit`, `.help`.
*   **Data Types (Dynamic Typing - more flexible, called "Type Affinity")**: `NULL`, `INTEGER`, `REAL`, `TEXT`, `BLOB`.
*   **SQL Syntax**: Largely standard SQL.
    *   `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`.
    *   `PRIMARY KEY AUTOINCREMENT` for auto-incrementing integer keys.
*   **Lite Queries**: Suitable for embedded applications, local data storage, caching.
*   **Transactions**: `BEGIN TRANSACTION; ... COMMIT;` or `ROLLBACK;`. (Atomic by default for single statements).
*   **Indexes**: `CREATE INDEX index_name ON table_name (column_name);`.
*   **Pragmas**: Special commands to modify SQLite operation or query internal data (e.g., `PRAGMA foreign_keys = ON;`).
*   **Storage**: Single file on disk.
*   **Use Cases**: Mobile apps, desktop apps, small websites, data analysis for small datasets.
*   **Limitations**: Limited concurrency (writer locks the entire database), no user management, fewer built-in functions compared to server-based RDBMS.
