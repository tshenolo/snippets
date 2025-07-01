# MySQL Cheatsheet

*   **Basic `mysql` client commands**: `SHOW DATABASES;`, `USE database_name;`, `SHOW TABLES;`, `DESCRIBE table_name;`, `EXIT;`.
*   **Data Types (Common)**:
    *   Numeric: `INT`, `BIGINT`, `SMALLINT`, `TINYINT`, `DECIMAL(M,D)`, `FLOAT`, `DOUBLE`. `AUTO_INCREMENT` for primary keys.
    *   String: `VARCHAR(N)`, `CHAR(N)`, `TEXT`, `BLOB`.
    *   Date/Time: `DATE`, `TIME`, `DATETIME`, `TIMESTAMP` (auto-updates by default).
    *   Boolean: `BOOL` or `BOOLEAN` (alias for `TINYINT(1)`).
    *   Enum: `ENUM('val1', 'val2', ...)`.
    *   JSON (MySQL 5.7+).
*   **SQL Queries** (largely same as PostgreSQL, minor syntax differences):
    *   `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `CREATE TABLE`, `ALTER TABLE`, `DROP TABLE`.
*   **Joins**: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`. (MySQL doesn't have `FULL OUTER JOIN` directly, emulated with `UNION`).
*   **Subqueries**: Queries nested inside another query (in `SELECT`, `FROM`, `WHERE`, `HAVING`).
*   **Aggregate Functions**: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, used with `GROUP BY`.
*   **Indexes**: `CREATE INDEX index_name ON table_name (column_name);`. `PRIMARY KEY`, `UNIQUE INDEX`, `FULLTEXT INDEX`.
*   **Storage Engines**: InnoDB (default, ACID, row-level locking, foreign keys), MyISAM (older, table-level locking).
*   **Optimization Tips**: Use appropriate data types, index columns used in `WHERE`/`JOIN`/`ORDER BY`, `EXPLAIN` query to analyze execution plan.
*   **User Management**: `CREATE USER`, `GRANT PRIVILEGES`, `REVOKE PRIVILEGES`.
