title: 001 MySQL Hello World
description: Learn the essential MySQL syntax, including creating databases, tables, and performing basic CRUD operations. Perfect for beginners!
keywords: MySQL syntax, MySQL tutorial, SQL basics, database commands, learn MySQL
date: 2024-12-17
tags:
  - MySQL
  - SQL
  - Database
categories: Database Tutorials
---

MySQL is a powerful relational database management system that uses SQL (Structured Query Language) to manage and query data. This guide focuses on the fundamental MySQL syntax, including how to create databases, design tables, and perform basic operations like inserting, querying, updating, and deleting data.

<!-- more -->
---

## 1. **Creating a Database**

To create a new database in MySQL, use the following command:

```sql
CREATE DATABASE my_database;
```

To select and start using the database:

```sql
USE my_database;
```

---

## 2. **Creating Tables**

Tables are the core structures in a relational database. Here's how to create a basic table:

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Explanation:
- `id`: A unique identifier with auto-increment.
- `name`: Stores the user's name, up to 100 characters.
- `email`: Ensures emails are unique for each user.
- `created_at`: Automatically stores the record's creation time.

---

## 3. **Inserting Data**

Add records to a table using the `INSERT INTO` command:

```sql
INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');
INSERT INTO users (name, email) VALUES ('Bob', 'bob@example.com');
```

---

## 4. **Querying Data**

Retrieve data from a table using the `SELECT` statement:

### Select All Records:
```sql
SELECT * FROM users;
```

### Select Specific Columns:
```sql
SELECT name, email FROM users;
```

### Adding Conditions with `WHERE`:
```sql
SELECT * FROM users WHERE name = 'Alice';
```

---

## 5. **Updating Data**

Modify existing records in a table with the `UPDATE` command:

```sql
UPDATE users SET email = 'alice.new@example.com' WHERE name = 'Alice';
```

---

## 6. **Deleting Data**

Remove records from a table using the `DELETE` statement:

```sql
DELETE FROM users WHERE name = 'Bob';
```

---

## 7. **Additional SQL Concepts**

### Sorting Results (`ORDER BY`):
```sql
SELECT * FROM users ORDER BY created_at DESC;
```

### Filtering Results (`LIMIT`):
```sql
SELECT * FROM users LIMIT 5;
```

### Counting Records:
```sql
SELECT COUNT(*) AS user_count FROM users;
```

---

## 8. **Combining Data with Joins**

To retrieve data from multiple tables, use `JOIN`:

```sql
SELECT users.name, orders.order_date
FROM users
JOIN orders ON users.id = orders.user_id;
```

---

## 9. **Dropping Databases or Tables**

### Deleting a Table:
```sql
DROP TABLE users;
```

### Deleting a Database:
```sql
DROP DATABASE my_database;
```

---

## Conclusion

This guide covers the essential MySQL commands needed to start working with databases. By practicing these operations, you'll develop a strong foundation in SQL and MySQL. Continue exploring advanced features like indexing, stored procedures, and query optimization to further enhance your database skills.
