# PostgreSQL Cheatsheet

*   **Basic `psql` commands**: `\l` (list DBs), `\c dbname` (connect), `\dt` (list tables), `\d table` (describe table), `\q` (quit).
*   **Data Types (Common)**:
    *   Numeric: `INTEGER`, `BIGINT`, `SMALLINT`, `NUMERIC(precision, scale)`, `REAL`, `DOUBLE PRECISION`, `SERIAL` (auto-incrementing int).
    *   Character: `VARCHAR(n)`, `CHAR(n)`, `TEXT`.
    *   Date/Time: `DATE`, `TIME`, `TIMESTAMP` (with/without time zone), `INTERVAL`.
    *   Boolean: `BOOLEAN`.
    *   JSON: `JSON`, `JSONB` (binary, more efficient, supports indexing).
    *   Array: `datatype[]` (e.g., `INTEGER[]`).
*   **Common Queries (SQL)**:
    *   `SELECT column1, column2 FROM table_name WHERE condition ORDER BY column LIMIT count OFFSET skip;`
    *   `INSERT INTO table_name (column1, column2) VALUES (value1, value2);`
    *   `UPDATE table_name SET column1 = value1 WHERE condition;`
    *   `DELETE FROM table_name WHERE condition;`
    *   `CREATE TABLE table_name (column_name DATATYPE constraints, ...);` (Constraints: `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `DEFAULT`, `CHECK`).
    *   `ALTER TABLE table_name ADD COLUMN ...`, `DROP COLUMN ...`, `ALTER COLUMN ... TYPE ...`.
    *   `DROP TABLE table_name;`
*   **Joins**: `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL OUTER JOIN`.
*   **Aggregate Functions**: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `GROUP BY`.
*   **Indexes**: `CREATE INDEX index_name ON table_name (column_name);` (Types: B-tree, Hash, GiST, GIN). Improves query performance.
*   **Transactions**: `BEGIN; ... COMMIT;` or `ROLLBACK;`.
*   **Views**: `CREATE VIEW view_name AS SELECT ...;`.
