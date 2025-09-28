##   DLEHI'S CHOLE BHATURE ARE  THE BEST . 








oined to Table B. An inner join:**  
    Displays rows where keys match.

48. **Can you join 3 tables together with inner join:**  
    Yes.  
    *Example:*  
    ```sql
    SELECT * FROM faculty f 
    INNER JOIN division d ON f.division_id = d.id 
    INNER JOIN country c ON f.country_id = c.id;
    ```

49. **Can you join a table to itself?**  
    Yes, SELF JOIN.  
    *Example:*  
    ```sql
    SELECT a.name, b.name FROM employees a, employees b WHERE a.manager_id = b.id;
    ```

50. **Which of the following is true about Cartesian Products?**  
    Formed without join condition (CROSS JOIN). Results in m*n rows.  
    *Example:*  
    ```sql
    SELECT * FROM table1 CROSS JOIN table2;
    ```

51. **In relational algebra the INTERSECTION of two sets (set A and Set B) corresponds to**  
    A AND B (common rows). Use INTERSECT.  
    *Example:*  
    ```sql
    SELECT * FROM set1 INTERSECT SELECT * FROM set2;
    ```

52. **In relational algebra the UNION of two sets (set A and Set B) corresponds to**  
    A OR B (combined, distinct). SELECTs must match columns/types/order.

53. **What is the difference between UNION and UNION ALL?**  
    UNION: distinct rows; UNION ALL: all rows (duplicates included). UNION ALL is faster.

54. **Having a list of Customer Names that searched for product 'X' and a list of customer Names that bought the product 'X'. What set operator would you use to get only those who are interested but did not bought product 'X' yet?**  
    MINUS (or EXCEPT in some DBMS).  
    *Example:*  
    ```sql
    SELECT name FROM searchers MINUS SELECT name FROM buyers;
    ```

## Section 4: Subqueries and Advanced Queries

### Theory
Subqueries are nested queries in SELECT/FROM/WHERE. Types: scalar (single value), row (multiple), correlated (depends on outer). Use for filtering, calculations. CASE for conditional logic. Functions like UPPER, CEILING for data transformation.

**Best Practices:**
- Use subqueries sparingly; joins often perform better.
- Correlated subqueries can be slow—optimize with EXISTS.
- Nest carefully to avoid performance hits.

### Examples
Subquery in WHERE:
```sql
SELECT * FROM products WHERE price > (SELECT AVG(price) FROM products);
```

CASE:
```sql
SELECT name, 
CASE WHEN age < 18 THEN 'Minor' ELSE 'Adult' END AS status 
FROM users;
```

### Q&A Bank (Questions 55-60)
55. **One (or more) select statement whose return values are used in filtering conditions of the main query is called**  
    Subquery (inner/nested query).

56. **Subqueries can be nested from the outer query is called a**  
    Correlated subquery (depends on outer row).  
    *Example:*  
    ```sql
    SELECT * FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE department = e.department);
    ```

60. **What is Case Function?**  
    Conditional logic like IF-THEN-ELSE.  
    *Example above.*

## Section 5: Data Definition and Manipulation (DDL, DML, DCL)

### Theory
DDL: Defines structures (CREATE, ALTER, DROP). DML: Manipulates data (INSERT, UPDATE, DELETE, SELECT—sometimes DQL). DCL: Controls access (GRANT, REVOKE). TRUNCATE (DDL) removes all rows without logging.

**Best Practices:**
- Use transactions with DML for rollback.
- Specify columns in INSERT for robustness.
- TRUNCATE for fast bulk deletes (no WHERE).

### Examples
CREATE TABLE:
```sql
CREATE TABLE customers (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL
);
```

INSERT:
```sql
INSERT INTO customers (name) VALUES ('John Doe');
```

### Q&A Bank (Questions 61-91)
61. **What are different types of statements supported by SQL?**  
    DDL (CREATE/ALTER/DROP), DML (INSERT/UPDATE/DELETE/SELECT), DCL (GRANT/REVOKE). SELECT sometimes in DQL.

62. **Which of the following SQL statements are DDL**  
    ALTER, CREATE, DROP, TRUNCATE TABLE.

63. **DML includes the following SQL statements**  
    SELECT, INSERT, UPDATE, DELETE.

64. **Grant and Revoke commands are under**  
    DCL.

65. **Which of the following is not a DML statement?**  
    COMMIT (transaction control, TCL).

66. **Which SQL statement is used to insert new data in a database?**  
    INSERT INTO.

67. **When inserting data in a table do you have to specify the list of columns you are inserting values for?**  
    No, if providing values for all columns in order. But best to specify for clarity.

68. **With SQL, how can you insert a new record into the "Customers" table?**  
    ```sql
    INSERT INTO Customers VALUES (1, 'John', 'Doe');
    ```

69. **With SQL, how can you insert "Hawkins" as the "LastName" in the "Customers" table?**  
    ```sql
    INSERT INTO Customers (LastName) VALUES ('Hawkins');
    ```

70. **How do you create a temporary table in MySQL?**  
    ```sql
    CREATE TEMPORARY TABLE temp_customers SELECT * FROM customers LIMIT 10;
    ```  
    Drops at session end.

71. **Which SQL statement is used to update data in a database?**  
    UPDATE.

72. **What is the keyword is used in an UPDATE query to modify the existing value?**  
    SET.

73. **How can you change "Jackson" into "Hawkins" in the "LastName" column in the Customer table?**  
    ```sql
    UPDATE Customers SET LastName = 'Hawkins' WHERE LastName = 'Jackson';
    ```

74. **Which SQL statement is used to delete data from a database?**  
    DELETE.

75. **With SQL, how can you delete the records where the "FirstName" is "John" in the Customers Table?**  
    ```sql
    DELETE FROM Customers WHERE FirstName = 'John';
    ```

76. **The FROM SQL keyword is used to**  
    Specify source table(s) in SELECT/UPDATE/DELETE/INSERT.

77. **What is the difference between DELETE and TRUNCATE?**  
    DELETE (DML): Row-by-row, loggable, WHERE clause, rollback possible. TRUNCATE (DDL): Bulk remove all rows, faster, no WHERE, resets auto-increment.

78. **Which SQL statement is used to create a table in a database?**  
    CREATE TABLE.

79. **What is Collation in SQL?**  
    Rules for comparing/sorting strings (e.g., case-sensitive). Character sets define symbols; collations define comparisons.  
    *Example:* Binary (simple encoding), case-insensitive.

80. **What is true about an AUTO_INCREMENT column in SQL?**  
    Generates unique numbers automatically on INSERT. Often PRIMARY KEY.  
    *MySQL Example:*  
    ```sql
    CREATE TABLE persons (id INT AUTO_INCREMENT PRIMARY KEY);
    ```

81. **What are valid constraints in MySQL?**  
    NOT NULL, UNIQUE, PRIMARY KEY (UNIQUE + NOT NULL), FOREIGN KEY, CHECK, DEFAULT, INDEX.

82. **Which of the following is NOT TRUE about constraints?**  
    All are true: Constraints enforce data integrity.

83. **The NOT NULL constraint enforces a column to not accept null values.**  
    True.

84. **An unique (non-key) field**  
    UNIQUE constraint (allows multiples per table, unlike PRIMARY KEY).

85. **What is CHECK Constraint?**  
    Limits values (e.g., age >= 18).  
    *Example:*  
    ```sql
    CREATE TABLE persons (age INT CHECK (age >= 18));
    ```

86. **What is the difference between UNIQUE and PRIMARY KEY constraints?**  
    PRIMARY KEY: UNIQUE + NOT NULL, one per table. UNIQUE: Multiple per table, allows NULLs (in some DBMS).

87. **What does SQL DROP TABLE clause do?**  
    Removes table and data.  
    ```sql
    DROP TABLE table_name;
    ```

88. **What is the difference between DROP and TRUNCATE?**  
    DROP removes table structure; TRUNCATE removes data only.

89. **How do you add a 'order_date' column to a table called 'order'?**  
    ```sql
    ALTER TABLE `order` ADD order_date DATE;
    ```

90. **What the correct syntax to rename column 'Address' to 'Addr' in 'Customer' table?**  
    ```sql
    ALTER TABLE Customer CHANGE Address Addr VARCHAR(50);
    ```

91. **Consider the following schema ADDRESSES (id, street_name, number, city, state) Which code snippet will alter the table ADDRESSES and delete the column named CITY?**  
    ```sql
    ALTER TABLE addresses DROP COLUMN city;
    ```

## Section 6: Indexes, Privileges, and Security

### Theory
Indexes speed queries like a book index. Clustered (reorders table), non-clustered (separate). Privileges: GRANT/REVOKE for access. SQL Injection: Malicious input exploiting queries.

**Best Practices:**
- Index frequently queried columns, but not all—updates slow them.
- Use prepared statements to prevent injection.
- Least privilege principle for users.

### Examples
Index:
```sql
CREATE INDEX idx_name ON customers (name);
```

GRANT:
```sql
GRANT SELECT ON database.* TO 'user'@'localhost';
```

### Q&A Bank (Questions 92-96, 115)
92. **What are Indexes in SQL?**  
    Speed retrieval. Duplicate allowed unless UNIQUE.  
    *Best Practice:* Update sparingly on insert-heavy tables.

93. **What is the difference between clustered and non-clustered indexes? Which of the following statements are true?**  
    Clustered: One per table, reorders data. Non-clustered: Multiple, separate structure. Clustered faster for reads; both true statements apply.

94. **The statement for assigning access privileges is**  
    GRANT/REVOKE.

95. **How many types of Privileges are available in SQL?**  
    System (e.g., CREATE TABLE), Object (e.g., SELECT on specific table).

96. **List the various privileges that a user can grant to another user?**  
    SELECT, INSERT, UPDATE, DELETE, EXECUTE, etc.

97. **What is SQL Injection?**  
    Code injection via input. Prevent with parameterized queries.  
    *Example Vulnerability:*  
    ```sql
    -- Bad: SELECT * FROM users WHERE id = '$input';  -- Input: ' OR '1'='1
    ```  
    *Safe:* Use placeholders.

## Section 7: Transactions and Concurrency

### Theory
Transactions ensure ACID: Atomicity (all or nothing), Consistency (valid states), Isolation (concurrent independence), Durability (persists after commit). Controls: COMMIT, ROLLBACK, SAVEPOINT. Locking prevents conflicts. Isolation levels: READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ (MySQL default), SERIALIZABLE.

**Best Practices:**
- Keep transactions short to reduce locking.
- Use explicit BEGIN TRANSACTION in multi-statement ops.
- Handle deadlocks with retries.

### Diagrams
ACID Properties (Text):
- Atomicity: Commit or Rollback entire tx.
- Isolation: Tx1 | Tx2 (no interference).

### Examples
Transaction:
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### Q&A Bank (Questions 97-104)
97. **What does the term 'locking' refer to?**  
    Prevents concurrent changes/reads on data.

98. **What are a transaction's main controls?**  
    COMMIT (save), ROLLBACK (undo), SAVEPOINT (partial rollback).  
    *Example:*  
    ```sql
    SAVEPOINT sp1;
    -- Operations
    ROLLBACK TO sp1;
    ```

99. **A transaction completes its execution is said to be**  
    Committed.

100. **Consider the following code: START TRANSACTION /transaction body/ COMMIT; ROLLBACK; What does Rollback do?**  
     Nothing—post-COMMIT changes are permanent.

101. **What are valid properties of the transaction?**  
     ACID.

102. **What happens if autocommit is enabled?**  
     Each statement auto-commits (default in MySQL).

103. **What is the default isolation level used in MySQL?**  
     REPEATABLE READ (prevents non-repeatable reads).

104. **In MySQL autocommit is enabled by default for each session.**  
     True.

## Section 8: Views, Stored Procedures, Triggers, and Advanced Topics

### Theory
Views: Virtual tables from queries. Updatable if simple. Cursors: Row-by-row processing in procedures. Triggers: Auto-execute on events (INSERT/UPDATE/DELETE). Optimization: Efficient plans via indexes, stats.

**Best Practices:**
- Use views for security (limit columns).
- Materialized views for performance (if supported).
- Triggers for audits, but avoid complex logic.

### Examples
View:
```sql
CREATE VIEW active_customers AS SELECT * FROM customers WHERE status = 'active';
```

Trigger:
```sql
CREATE TRIGGER after_insert AFTER INSERT ON orders FOR EACH ROW 
INSERT INTO audit_log VALUES (NEW.id, 'Inserted');
```

### Q&A Bank (Questions 105-114)
105. **Which of these is also known as a virtual table in MySQL?**  
     View.

106. **Are views updatable using INSERT, DELETE or UPDATE?**  
     Some are (simple, no aggregates/DISTINCT/GROUP BY). Conditions: One base table, includes PK, no subqueries.

107. **What are the advantages of Views?**  
     Simplify queries, limit access, hide complexity. Changes commit only after base table ops.

108. **Does a View contain data?**  
     No (normal view: query only). Yes for materialized (stored data, needs refresh).

109. **What SQL statement do you have to use to remove a view?**  
     ```sql
     DROP VIEW view_name;
     ```

110. **Can a View based on another View?**  
     Yes.

111. **Inside a stored procedure you to iterate over a set of rows returned by a query using a**  
     CURSOR. Steps: DECLARE, OPEN, FETCH, CLOSE, DEALLOCATE.

112. **How do you call the process of finding a good strategy for processing a query?**  
     Query optimization (considers plans, stats).

113. **What is a trigger? or There are triggers for… or A trigger is applied to**  
     Stored procedure auto-executing on DML/DDL events (INSERT/UPDATE/DELETE/CREATE/etc.). Components: Event, Action.  
     *Example above.*

114. **A special kind of a stored procedure that executes in response to certain action on the table like insertion, deletion or updation of data is called**  
     Trigger.

---

Resources

- www.wikipedia.org
- www.w3schools.com
- www.freefeast.info
